

# Lesson Release Process

This process has been created with the aim of disrupting as little as possible the current management of lesson repositories.

## Overview

As today, each lesson will live in its own repository, using a single branch named `gh-pages` (this way the latest version of the repository can be accessed anytime for preview by lesson developers, when we soon switch to Jekyll).

In addition, when a release has to be made, the lesson maintainer will tag the commit with, e.g., `v5.9`.

In addition, still in the lesson repository, the toplevel releaser, will make a `v5.9-html` tag by generating the HTML from `v5.9`.

In addition, there will be a single `swc-release` repository (with a single `gh-pages` branch), with a subfolder for each released version, e.g., `5.9`.
Each subfolder will contain an "index" page and a submodule pointing to each lesson, pointing to `v5.9-html`.
The result will be a website aggregating all the lessons (in the selected version) [ex53].


## Release process as steps

- *all*: decide that a new toplevel release (of all core lessons) will happen, give it a version number, e.g., `5.9`.
- (for each lesson) *lesson maintainers*:
    - check that the lesson is in a good shape
    - tag it with `v5.9`
- (for each lesson) *toplevel releaser*:
    - clone the lesson
    - make a new branch, `v5.9-html`
    - generate the HTML page and check it
    - commit the HTML
- *toplevel releaser*, in the `swc-release` repository (this step could be assisted by a script):
    - create a `5.9` subfolder
    - in this folder, for each lesson, add a submodule pointing to the `v5.9-html` tag/branch
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

## Tag vs Branch for `v5.9` and `v5.9-html`

Both have different advantages, and for now, it is quite balanced.

A tag has the advantage to remain fixed by default.
A branch has the advantage that it will avoid a commit-by-mistake of generated HTML in the `gh-pages` branch.


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
- 

## Possible more references

- https://github.com/swcarpentry/lesson-template/issues/62
- https://github.com/swcarpentry/lesson-template/issues/76
- https://github.com/twitwi/test-jekyll-multi-swc-4.3-fake/
- [ex53] Example with a few lessons in version 5.3:  http://twitwi.github.io/test-jekyll-multi-swc-4.3-fake/5.3/



