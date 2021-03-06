---
title: Building a Haskell Project
layout: en
permalink: haskell/
---

### What This Guide Covers

This guide covers build environment and configuration topics specific to Haskell projects. Please make sure to read our [Getting Started](/user/getting-started/) and [general build configuration](/user/build-configuration/) guides first.

## Overview

We currently have GHC 7.6.3, 7.4.2 , and 7.0.4 installed, with 7.6.3 being the default.

For full up-to-date list of provided tools, see
our [CI environment guide](/user/ci-environment/). Key build lifecycle commands (dependency installation, running tests) have
defaults that use `cabal`. It is possible to override them to use `make` or any other build tool and dependency management tool.

## Specifying the GHC version

You can specify one or more GHC versions:

```
ghc: 7.4
```

Multiple versions:

```
ghc:
  - 7.6
  - 7.4
```

It is recommended that you only use the major and minor versions to specify the version to use, as we may update the patchlevel releases at any time.

## Default Test Script

Default test script Travis CI Haskell builder will use is

    cabal configure --enable-tests && cabal build && cabal test

It is possible to override test command as described in the [general build configuration](/user/build-configuration/) guide, for example:

    script:
      - cabal configure --enable-tests -fFOO && cabal build && cabal test


## Dependency Management

### Travis CI uses cabal

By default Travis CI use `cabal` to manage your project's dependencies.

The exact default command is

    cabal install --only-dependencies --enable-tests

It is possible to override dependency installation command as described in the [general build configuration](/user/build-configuration/) guide,
for example:

    install:
      - cabal install QuickCheck


## Build Matrix

For Haskell projects, `env` and `ghc` can be given as arrays
to construct a build matrix.

## Examples

* [spockz/TravisHSTest](https://github.com/spockz/TravisHSTest/blob/master/.travis.yml)
* [ZeusWPI/12Urenloop](https://github.com/ZeusWPI/12Urenloop/blob/master/.travis.yml)
