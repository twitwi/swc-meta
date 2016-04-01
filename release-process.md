# Lesson Release Process

This document describes how Software Carpentry will manage releases of new versions of lessons.
This process has been designed to disrupt the current management of lesson repositories as little as possible.

## Overview

1. Each lesson will continue live in the `gh-pages` branch of its own repository.
2. When a release has to be made, the *lesson maintainer* (or maintainers) will create a branch named after the release, e.g., `v5.9`.
3. A *release maintainer* will generate HTML pages for that release and add them to the branch.
4. If there isn't already a directory for that release in the `swc-release` repository,
   the release maintainer will create one
   and add an `index.html` page to it.
5. The release maintainer will add a submodule to the release directory of `swc-release`
   that points to the newly-created release branch of the lesson.

## Elements

*  The `swc-release` repository
   * This repository contain one directory for each release, e.g., `v5.9`.
   *  Each release directory will contain one submodule for each lesson, e.g., `v5.9/shell-novice`.
   *  That submodule will refer to the release branch in the lesson's repository, e.g., `https://github.com/swcarpentry/shell-novice/tree/v5.9`.
*  The lesson maintainer(s)
   *  Same roles as at present.
*  The release maintainer
   *  A volunteer who handles the `swc-release` repository and the submodules therein.

## Discussion

*  Old versions of lessons are available online in perpetuity with predictable URLs.
   *  See <http://twitwi.github.io/test-jekyll-multi-swc-4.3-fake/5.3/> for proof that submodules show up properly in `github.io`
      provided the generated HTML has been committed to the branch.
*  No changes to our current day-to-day operations.
*  Only one person (at a time) needs to comprehend the profound mysteries of Git submodules.
*  Leaves open the option of switching to a pure-Jekyll process for active versions of lessons
   (i.e., for what's in each lesson's `gh-pages` branch).
   without requiring it.
*  Alternatives were unappealing:
   *  Create new repository for each release using `import` with its own `gh-pages` branch
      *  Would make it harder to copy fixes back and forth between versions
   *  Create sub-directory in each lesson's repository for each release, e.g., `shell-novice/v5.9`
      *  Repeated duplication of files
      *  Complicates management of layouts, paths to included files and images, etc.
      *  Doesn't isolate version safely
   *  Create sub-directory with only generated HTML and images
      *  Duplicate files again
      *  Doesn't support late-breaking fixes

## See Also

*   <https://github.com/swcarpentry/lesson-template/issues/62>
*   <https://github.com/swcarpentry/lesson-template/issues/76>
*   <https://github.com/twitwi/test-jekyll-multi-swc-4.3-fake/>
