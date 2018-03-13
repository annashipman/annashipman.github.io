---
anchor_id: travis-deploy
title: Deploying to shared hosting with Travis
layout: blog_post
---

The [SPA conference website](https://www.spaconference.org/) deploys to production automatically on merge to master. It is on shared hosting, and setting this up with [Travis](https://travis-ci.org/) was a bit tricky, so I'm blogging how I did it in case it's useful for others.

## The documentation on deploying to shared hosting is not very clear

Configuring Travis to deploy automatically on merge to master is pretty straightforward if you’re using a [supported provider](https://docs.travis-ci.com/user/deployment/). However, if you're using shared hosting, the documentation is not amazing.

I figured it out eventually by juggling between [a blog post](https://oncletom.io/2016/travis-ssh-deploy/) (this one is useful for explanations of how Travis works but less so for step-by-step), the [actual config that person uses](https://github.com/oncletom/oncletom.io/blob/master/.travis.yml), [another blog post](https://andreas.heigl.org/2016/06/07/automated-deploy-from-travis-ci-via-ssh/) (useful for some of the steps), the Travis docs on [encrypting files](https://docs.travis-ci.com/user/encrypting-files/), [custom deployment](https://docs.travis-ci.com/user/deployment/custom/) and [the build lifecycle](https://docs.travis-ci.com/user/customizing-the-build/#The-Build-Lifecycle), and [yet another blog post](http://ajaykarwal.com/deploying-jekyll-using-travis-ci/) (very useful for the actual config, but for a different set-up than I wanted).

That juggling made me think my addition to the genre was worth it.

## The steps I took

1. Follow [Travis's get started instructions](https://docs.travis-ci.com/user/getting-started/#To-get-started-with-Travis-CI) to sign in to Travis and add the repository you want to deploy.
1. Create a `.travis.yml` file. The inital one can just have the language and how to build the site.

    ```
    language: ruby
    rvm:
    - 2.3.3
    script: scripts/build.sh
    branches:
      only:
      - master
    ```
    {:.code-sample}

    You can tell Travis how to build the site inline, or call out to a build script as I have done.
    ```
    #!/bin/bash
    set -e

    bundle exec jekyll build
    ```
    {:.code-sample}
    The build script has to be executable (`chmod +x 600`).
1. Install travis locally (`gem install travis`), and, using the command line tool, [encrypt](https://docs.travis-ci.com/user/encryption-keys) any variables that you will use for deploy. For example, if you use FTP, you will want to encrypt at least the password.
    ```
    travis encrypt SOMEVAR="secretvalue" --add
    ```
    {:.code-sample}

    The `--add` flag in this command adds the [required lines](https://github.com/spaconference/spa-website/blob/3ed4b7c9d647d5c3cc5d90f746c9549883699a1d/.travis.yml#L8-L11) to your Travis file.
1. Write a deploy script: a script that describes the steps you take to deploy to shared hosting. For example, if you use FTP, then write the command that you would use to FTP the built site to the server. Instead of the variables you have encrypted, use `SOMEVAR`. 

    I use Rsync to deploy, and have encrypted the username and deploy host. You can see [the deploy script](https://github.com/spaconference/spa-website/blob/master/scripts/deploy.sh) on GitHub.

    This also needs to be executable.
1. Create a dedicated SSH key (no passphrase) for deploying. This makes it easy to to identify and revoke if necessary.

    ```
    ssh-keygen -t rsa -b 4096 -C 'build@travis-ci.org' -f ./deploy_rsa
    ```
    {:.code-sample}
1. Log in to command line Travis (`travis login`) and get Travis to [encrypt the private key file](https://docs.travis-ci.com/user/encrypting-files/). It prints a helpful output reminding you to only commit the `.enc` version NOT the `deploy_rsa` itself.

    ```
    travis encrypt-file deploy_rsa --add
    ```
    {:.code-sample}

    Again, the `--add` flag automatically adds the [required lines](https://github.com/spaconference/spa-website/blob/3ed4b7c9d647d5c3cc5d90f746c9549883699a1d/.travis.yml#L14-L16) to your Travis file.

    Commit the changes to `.travis.yml` and the `deploy_rsa.enc`.
1. Copy the public key to the remote host.

    ```
    ssh-copy-id -i deploy_rsa.pub <ssh-user>@<deploy-host>
    ```
    {:.code-sample}
1. Delete the public key and the private key as they are no longer needed; you only need the encrypted key.
    ```
    rm -f deploy_rsa deploy_rsa.pub
    ```
    {:.code-sample}
1. In the `before_install`, change the `out` location for the decrypted private key to `/tmp/` so it doesn't end up in any of the publically accessible directories, and make it executable.

    ```
    before_install:
    - openssl [snip...] -out /tmp/deploy_rsa -d
    - chmod 600 /tmp/deploy_rsa
    ```
    {:.code-sample}
1. In the same section, start the ssh agent and add the key to it.

    ```
    - eval "$(ssh-agent -s)"
    - ssh-add /tmp/deploy_rsa
    ```
    {:.code-sample}
1. Get `.travis.yml` to call the deploy script.

    This is an example of how the Travis docs could be clearer. You don't want to deploy if the build script fails, so you might want to call this in an `after_success` step as part of a [script deployment](https://docs.travis-ci.com/user/deployment/script), but in fact, this will do whatever you ask after every successful build. But in our case, we only want to actually deploy on merges to master, not on *any* successful build. For example, if we've just opened a PR and that builds successfully, we don't want that branch deployed to production.

    So what we actually want is [custom deployment](https://docs.travis-ci.com/user/deployment/custom/).

    ```
    deploy:
      provider: script
      script: scripts/deploy.sh
      skip_cleanup: true
      on:
        branch: master
    ```
    {:.code-sample}

    `skip_cleanup` is required because otherwise [Travis resets the working directory](https://docs.travis-ci.com/user/deployment#Uploading-Files-and-skip_cleanup), so you lose the artefects from the build (i.e. exactly what you want to deploy!)

## What my config looks like

The full `travis.yml` we've now created looks like this:

```
language: ruby
rvm:
- 2.3.3
script: scripts/build.sh
branches:
  only:
  - master
env:
  global:
  - secure: qvSoY270qAXOtmWdRio9vvhLEf5HHdyzMS39yS4yZw74[snip for length]
  - secure: Hr7FV7lHFEblYfn7EYM/4qV3qV8zdHLebXzNyRvP8L/U[snip for length]
before_install:
- openssl aes-256-cbc -K $encrypted_ed2cb1b127e1_key -iv $encrypted_ed2cb1b127e1_iv
  -in deploy_rsa.enc -out /tmp/deploy_rsa -d
- chmod 600 /tmp/deploy_rsa
- eval "$(ssh-agent -s)"
- ssh-add /tmp/deploy_rsa
deploy:
  provider: script
  script: scripts/deploy.sh
  skip_cleanup: true
  on:
    branch: master
```
{:.code-sample}

## Further information

This (allegedly deprecated but still working) [`travis.yml` linter](http://lint.travis-ci.org/) is useful.

Have a look at the [SPA website Travis file](https://github.com/spaconference/spa-website/blob/master/.travis.yml) and [the builds](https://travis-ci.org/spaconference/spa-website/builds/) if you'd like to know more about how it works for us.
