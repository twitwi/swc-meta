

# Lesson Release Process

This process has been created with the aim of disrupting as little as possible the current management of lesson repositories.

## Overview

As today, each lesson will live in its own repository, using a single branch named `gh-pages`.
If we switch to Jekyll (discussions are in progress), we get a big advantage: the latest version of the lesson can always be accessed for preview by lesson developers.

In addition, when a release has to be made, the *lesson maintainer* will mark the version by creating a branch, e.g., `v5.9`.

Still in the lesson repository, the *toplevel releaser*, will generate the HTML pages on the branch, e.g., `v5.9`.

In addition, there will be a single `swc-release` repository (with a single `gh-pages` branch), with a subfolder for each released version, e.g., `5.9`.
Each subfolder will contain an "index" page and a submodule pointing to each lesson, pointing to branch `v5.9`.
The result will be a website aggregating all the lessons (in the selected version) [ex53].


## The process

- *all*: decide that a new toplevel release (of all core lessons) will happen, give it a version number, e.g., `5.9`.
- (for each lesson) *lesson maintainers*:
    - check that the lesson is in a good shape
    - make a branch named `v5.9`
- (for each lesson) *toplevel releaser*:
    - clone the lesson
    - switch to the `v5.9` branch
    - generate the HTML page and check/validate it
    - commit the HTML and push
- *toplevel releaser*, in the `swc-release` repository (this step could be assisted by a script):
    - create a `5.9` subfolder
    - in this folder, for each lesson, add a submodule pointing to the `v5.9` tag/branch
    - create an index file
    - commit and push
- *toplevel releaser*: check the online version
- *website maintainer*:
    - check the online version
    - add/update links on the website

----------------------------------------

# When to release?

TBD


----------------------------------------

# Vocabulary

- *toplevel release*: release of a group core lessons, together (e.g., release 5.3).
- *toplevel releasers*: maintainers responsible for the *toplevel releases*.


# Discussions

## About having a single release repository versus one per release

At least, simpler to manage.
TBD


## About custom intermediary releases

TBD

- trade off between unstable vs "old" version
- can use release scripts to help
- may need to copy the generated HTML instead of only submodules

## About HTML files and the impossibility to nest Jekyll roots

Even if it would have been very nice to avoid committing generated html files in the repositories, we do this for multiple reasons:

- Jekyll (that generates gh-pages dynamically) does not handle multiple subfolders with different configurations and thus is unable to handle an aggregation of multiple lessons.
- Committing generated files, for a release, makes sense as it keeps a version that we are sure will work even if Jekyll is updated in a non-backward-compatible manner.
- Our old process (v5.3) does use pandoc and not jekyll.

## About using submodules

Sub-modules are a complex git feature and can be tricky to use.
This is especially true when they need to be updated.

Here is the rationale for using submodules for releases:

- Submodules must only be manipulated by toplevel releasers (not by lesson maintainers, authors or instructors).
- Submodules will never be updated.
- Submodules allow us to avoid copying HTML files: what we see (in the release repo) is what we have (in the lesson repo).


## Possible more references

- https://github.com/swcarpentry/lesson-template/issues/62
- https://github.com/swcarpentry/lesson-template/issues/76
- https://github.com/twitwi/test-jekyll-multi-swc-4.3-fake/
- [ex53] Example with a few lessons in version 5.3:  http://twitwi.github.io/test-jekyll-multi-swc-4.3-fake/5.3/



