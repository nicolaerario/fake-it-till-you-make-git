---
layout: page
title: Fantastic Features and where to work them
---

> "This flow starts with **`issues`** and is a way to make the relation between the code and the issue tracker more transparent."  
> "If you are thinking about a new feature or if you think you have found a bug, search first for it in the `issues`; it can be that it's already tracked an someone else is working on it".

## _TLDR;_ Use it as a quick recap. Make sure to read the [detailed version](#detailed-version)

1. Open an `issue` for the feature or bug you have to work on
2. Create a branch with the name starting with the issue number: `20-fantastic-feature`
3. Work on your branch
4. When your work is complete, make sure your branch isn't behind the `default` branch (this will assure a clean history and will avoid merge conflicts to the reviewers); if your branch is behind default, then rebase it on default
5. Create a pull request ([see Pull request flow](#pull-request-flow)) and assign a reviewer to it; make sure to include `closing keywords` to refer issues you are working on ([see Linking and closing issues from pull requests](#linking-and-closing-issues-from-pull-requests))

## Detailed Version

### Issues

Any significant change to the code should start with an **`issue`** that describes the goal. Having a reason for every code change, helps to inform the rest of the team and to keep the scope of a `feature branch` small.

> "Each change to the codebase starts with an issue in the issue tracking system."

If you are faced with a bug, a regression, etc, search for a related issue first; then, if not present, open one.  
_Raising an issue is part of the development process because they can be used in sprint planning and time estimates._  
The issue title should describe the desired state of the system.
For example, the issue title _"As an administrator, users can be removed without receiving an error"_ is better than _"Administrators can’t remove users."_  
Issues can be documented with "steps to reproduce" and media files like `screenshots` or `gifs`.

### Working with feature branches

When you are ready to code, create a branch for the issue from the **`default`** branch. This branch will be the place for any work related to this change.
If you know before you start that your work depends on another branch, you can also branch from there.

> "N.B. : the **`default`** branch in a repository is the `base` branch for new pull requests and code commits. GitHub counts commits as contributions only when them are merged to the base branch"

Naming the branch with a reference to the related issue can be a good practice
(ex.: `20-this-is-a new-feature` , where `20` is the issue reference number).

> Both **GitHub** and **GitLab** offer the possibility to open a branch directly from the issue page: this can be a time saver since the branch will be based on default branch and it will have the issue number at the beginning of the name; the only precaution is to arrange the name so that it is declarative but not too long.

### Commit often and push frequently

A good way to make your development work easier is to `commit` often. Every time you have a working set of tests and code, you should make a commit. Splitting up work into individual commits provides context for developers looking at your code later. Smaller commits make it clear how a feature was developed. They help you roll back to a specific good point in time, or to revert one code change without reverting several unrelated changes.
Committing often also helps you **share your work**, which is important so that _everyone is aware of what you are working on._ You should push your feature branch frequently, even when it is not yet ready for review.

> By sharing your work in a feature branch or a pull request, you prevent your team members from duplicating work. Sharing your work before it's complete also allows for discussion and feedback about the changes. This feedback can help improve the code before it gets to review.

When you are done or want to discuss the code, open a **`pull request`**.

> "A pull request is an online place to discuss the change and review the code."

While working on a branch, it's always a good idea to pay attention to the evolutions of the branch from which you started. At the end of the work, before creating a PR, it would be preferable to "update" your feature branch with the new commits of the parent via a rebase. This will ensure a linear commit history and also that the reviewer will not have to deal with (unpleasant) merge conflicts.

### Pull Request flow

**`Pull requests`** are created in a Git management application. They ask an assigned person to merge two branches.  
If you work on a `feature` branch for more than a few hours, share the intermediate result with the rest of your team. To do this, create a pull request without assigning it to anyone. Instead, mention people in the description or a comment (for example `@nicolaerario, wdyt about this..?`). This indicates that the pull request is not ready to be merged yet, but feedbacks are welcome.

When you open the pull request but do not assign it to anyone, it is a **`draft pull request`**. These are used to discuss the proposed implementation but are not ready for inclusion in the default branch yet. Start the title of the pull request with `[Draft]`, `Draft:` or `(Draft)` can help to prevent it from being merged before it’s ready.

> "With GitHub you can _mark_ a PR as Draft to prevent to be accidentally merged"

Your team members can comment on the pull request in general or on specific lines _with line comments_. The pull request serves as a code review tool, and no separate code review tools should be needed. If the review reveals shortcomings, anyone can commit and push a fix. Usually, the person to do this is the creator of the pull request. The diff in the pull request automatically updates when new commits are pushed to the branch.

When you think the code is ready, assign the pull request to a **`reviewer`** (usually the person who knows most about the codebase you are changing). Also mention any other people from whom you would like feedback. The reviewers can merge the changes when they think the code is ready for inclusion in the `default` branch. If they find something wrong and that needs to be fixed, they can request more `changes` (or `close` the pull request without merging).

Pull requests **always create a merge commit**, even when the branch could be merged without one. This merge strategy is called **`no fast-forward`** in Git. After the merge, delete the feature branch, _because it is no longer needed_.  
Suppose that a branch is merged but a problem occurs and the issue is reopened. In this case, it is no problem to reuse the same branch name, because the first branch was deleted when it was merged. At any time, there is at most one branch for every issue. It is possible that one feature branch solves more than one issue.

### Linking and closing issues from pull requests

You can **`link`** an issue to a pull request manually or using a supported keyword in the pull request description.
When you merge a linked pull request into the default branch of a repository, its linked issue is **automatically closed**.
You can link a pull request to an issue by using a `supported keywords` in the pull request's description or in a commit message (**please note that the pull request must be against the default branch**).

**GitHub closing keywords:**

- close
- closes
- closed
- fix
- fixes
- fixed
- resolve
- resolves
- resolved

If you use a closing keyword to reference a pull request comment in another pull request, the pull requests will be linked. Merging the referencing pull request will also close the referenced pull request.

The syntax for closing keywords depends on whether the issue is in the same repository as the pull request.

| Issue in the same repository    | KEYWORD #ISSUE-NUMBER                 | Closes #10                                                   |
| ------------------------------- | ------------------------------------- | ------------------------------------------------------------ |
| Issue in a different repository | KEYWORD OWNER/REPOSITORY#ISSUE-NUMBER | Fixes octo-org/octo-repo#100                                 |
| Multiple issues                 | Use full syntax for each issue        | Resolves #10, resolves #123, resolves octo-org/octo-repo#100 |

Only manually linked pull requests can be manually unlinked. To unlink an issue that you linked using a keyword, you must edit the pull request description to remove the keyword.

You can also use closing keywords in a commit message. The issue will be closed when you merge this commit into the default branch, but the pull request that contains the commit will not be listed as a linked pull request.
