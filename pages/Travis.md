---
autogenerated: true
title: Travis
breadcrumb: Travis
layout: page
author: test author
categories: Development
description: test description
---

[Travis CI](https://travis-ci.org/) is a tool for [continuous
integration](Project_management#Continuous_integration "wikilink"). It
has excellent integration with [GitHub](GitHub "wikilink"), and is very
useful for automating builds, deployment and other tasks. 

# Services

[ImageJ](ImageJ "wikilink") and [SciJava](SciJava "wikilink") projects
use Travis in a variety of ways:

  - Perform builds of SciJava projects. Travis deploys `SNAPSHOT` builds
    to the [SciJava Maven repository](https://maven.scijava.org/) in
    response to pushes to each code repository's `master` branch. So any
    downstream projects depending on a version of `LATEST` for a given
    component will match the last successful Travis build—i.e., the
    latest code on `master`.
  - Run each project's associated [unit
    tests](wikipedia:Unit_testing "wikilink"). Travis is instrumental in
    early detection of new bugs introduced to the codebase.
  - Perform [releases](releases "wikilink") of
    [SciJava](SciJava "wikilink") projects. Travis deploys release
    builds to the appropriate Maven repository—typically either the
    SciJava Maven repository or [OSS
    Sonatype](https://oss.sonatype.org/).
  - Keep the [javadoc](javadoc "wikilink") site updated.
  - Keep other web resources updated.

# Automatic Deployment of Maven Artifacts

Deploying your library to a [Maven](Maven "wikilink") repository makes
it available for other developers. It is also a [contribution
requirement for the Fiji
project](Fiji/Contribution_requirements "wikilink").

## Requirements

  - Host your [open-source](open-source "wikilink") project on
    [GitHub](GitHub "wikilink").
  - Log in to [Travis CI](https://travis-ci.com/auth) with your
    corresponding GitHub account and enable your repository.
  - Contact an ImageJ admin in [Gitter](Chat#Gitter "wikilink") or [the
    Image.sc Forum](http://forum.image.sc/) and request that they file a
    PR which adds Travis support to your repository.

## Instructions

In order to add Travis CI support to a repository, the SciJava
credentials are needed: A) for deploying to Maven repositories; and B)
in the case of deploying to OSS Sonatype, for GPG signing of artifacts.
If you have a copy of these credentials, and admin access to the
relevant repository on GitHub, you can use the [travisify.sh
script](https://github.com/scijava/scijava-scripts/blob/master/travisify.sh)
to perform the needed operations. This script requires the [travis
command line client](https://github.com/travis-ci/travis.rb) to be
installed, and you may need to run `travis login` to authenticate first.
If you need help, please ask [on the Image.sc
Forum](https://forum.image.sc/) in the Development category, or in the
[scijava-common channel](https://gitter.im/scijava/scijava-common) on
Gitter.

## Testing things which cannot run headless

If your tests require a display (i.e.: they do not pass when run
[headless](headless "wikilink")), you can use [Xvfb](Xvfb "wikilink") as
follows:

``` yml
before_script:
  - "export DISPLAY=:99.0"
  - "sh -e /etc/init.d/xvfb start"
  - sleep 3 # give xvfb some time to start
```

Of course, you should do this only as a last resort, since the best unit
tests should not require a display in the first place.

[Category:Development](Category:Development "wikilink")