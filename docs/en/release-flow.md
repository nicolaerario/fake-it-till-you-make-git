---
layout: page
title: Release the power of your code!
description: Organize the code into versions release
---

> Releases are created to bundle and deliver iterations of a project;  
> they are based on Git `tags`, which mark a specific point in the repository's history.

## Creating a release

When the code on `develop` branch is stable and ready for a new release:

1. Update files like `CHANGELOG.md` and project configuration (`package.json` for example) _(if any, otherwise go to step 3)_:

   - In the `package.json` only the version number changes (see [Versioning](#versioning))
   - the `changelog` is filled by the list of all **PR's** from the latest release till now; the list can be grouped by scope (fix, change, new feature).

   > _Tip_: Even if we are not actually going to release at this exact point, we can use the feature that `GitHub` provides on the `Release page` to generate our changelog: just give a temporary tag, put our `develop` branch as the _target_, and click on `Generate release notes` button

2. `Push` this small update with no business logic **directly to develop branch**, without any PR (usually with a commit message like: `Bump version to v0.0.1`).  
   _We will make sure that the `dev CI/CD` pipeline won't be triggered by this merge.(see [CI/CD - wip not ready yet](#))_
      <!-- TODO: Add reference to CI/CD -->

   > _Note_: To perform direct push on a `long-lived branch` such as `develop`, you must have the _right role permissions_ or the branch must not have _protection rules_ that do not allow direct push. _Even if they are simple textual changes, we must always be careful making direct push on long-lived branches._

      <!-- TODO: Add reference to roles and protection rules -->

3. Make a PR from `develop` to `master` branch, naming it as `Release <tag name>` (_Release v0.0.1_ for example).

4. After the PR is merged to `master` branch, create a git `tag` locally:

   - Switch to `master` branch (the long-lived branch used for the releases) and pull changes
   - Create an `annotated tag` with `git tag -a v0.0.1 -m "Release v0.0.1"`
   - Now push the `local tag` to **remote** with `git push origin v0.0.1`

   Pushing the `tag` can be useful to trigger the _staging/testing_ `CI/CD pipeline` (see [CI/CD - wip not ready yet](#))
   <!-- TODO: Add reference to CI/CD -->

5. If tests passes (your _smoke test_, test suites, test by human tester, etc.) and no other bugfix are needed, from GitHub `Releases` page click on the `Create a new release` button:

   - select the previous created `tag`
   - put the same tag name as title of the release
   - use `Auto generate release notes` to generate the release changelog from the list of PR's
   - `Publish` the release 🏆

6. At this point, switching to `develop` branch we are _behind_ `master` by 1 commit (the Release PR, remenber you?):  
   make `git merge origin/master` and then `git push` to realign both branches at the same commit (local and remote). _(see the note below)_

> In this moment the `release` (the tag), `master` and `develop` branches points **exactly** at the same commit in the history

_**Note:** point `6` is needed because in the repo we have the branch `develop` set as the `working` branch (from where all new feture branches will start) while `master` is the `release` branch_

## Versioning

It's a good practice to use a valid versioning convention.  
One of the most widely used (and the one I prefer) is [Semantic Versioning](https://semver.org/ 'Semantic Versioning')

So, given a version number `MAJOR.MINOR.PATCH`, increment the:

1. `MAJOR` version when you make incompatible API changes (_breaking changes_)
2. `MINOR` version when you add functionality in a backwards compatible manner (_new feature_)
3. `PATCH` version when you make backwards compatible bug fixes (_bugfix_)
