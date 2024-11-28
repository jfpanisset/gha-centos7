# GitHub Actions with CentOS 7 based containers

Earlier in 2024 then GitHub Actions runner started defaulting to
a build of NodeJS 20 linked against glibc 2.27, which would
then fail to execute in containers based on CentOS 7, which
is based on glibc 2.17.

This is problematic for [aswf-docker](https://github.com/AcademySoftwareFoundation/aswf-docker)
images for the [VFX Platform 2022 and older](https://vfxplatform.com) which specifies glibc 2.17.

Until November 2024 the environment variable `ACTIONS_RUNNER_FORCE_ACTIONS_NODE_VERSION: node16`
could be used to force the GitHub Actions runner to keep using the NodeJS 16 binary linked against
glibc 2.17, but this no longer works.

This repo demonstrates how to use "unofficial" NodeJS builds such as
[node-v20.18.1-linux-x64-glibc-217.tar.gz](https://unofficial-builds.nodejs.org/download/release/v20.18.1/node-v20.18.1-linux-x64-glibc-217.tar.gz)
to allow 2022 and older `aswf-docker` images to keep running.

Based on:

https://github.com/actions/runner/issues/2906
https://github.com/dixyes/ghactionsplay/blob/main/.github/workflows/glibc217node20.yml
