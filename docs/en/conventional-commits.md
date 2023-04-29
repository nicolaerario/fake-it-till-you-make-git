---
layout: page
title: Why your history is like a fix...fax...fox?
description: Some conventions on commit messages (and PR titles)
---

> Conventional commits is a method to write commit messages in a meaningful way.

There are many benefits to adopting `conventional commits`. But the first thing that an adopter notices is that they simplify the process of _writing a **good** commit message_.

All developers are aware how _difficult_ it can be to name things, and writing descriptive yet succinct commits can be even more difficult. By providing a format to follow, conventional commits take away a lot of the thinking work that is required when writing a commit message, and point us in a good direction.

The first thing you need to do before writing a commit message is to ask yourself: **_"This commit will..."_** and then complete the sentence with your commit message.

The result would be like this: `add a new feature in my code` (**attention please**: its an example, **really!**).

After you write a meaningful commit title, you can (it's not obbligatory) expand with a body to better explain details that cannot fit into 50 characters.  
Start to write the body **always after a new line**.

> You don't need to mention the file where you change the code or other things that can be told you by `git`; focus only on _what_ your code do.

Following the conventions drawn up by [conventionalcommits.org](https://www.conventionalcommits.org/), I've derived mine.  
The commit message should be structured as follows:

```
<type>[optional scope]: <description>

[optional body]

```

## Types

- **Fix**: a commit of the type `fix` patches a bug in your codebase.
- **Feat**: a commit of the type `feat` introduces a new feature to the codebase.
- **Refactor**: a commit of the type `refactor` introduces a refactor to the codebase.
- **BREAKING CHANGE**: a commit that append `!` after the type/scope, introduces a breaking API change. A BREAKING CHANGE can be part of commits of any type.

Types other than `Fix:`, `Feat:` and `Refactor:` are allowed, for example: `Build:`, `Ci:`, `Docs:`, `Style:`, `Test:`, and others.

Some examples:

```
fix: Prevent racing of requests
feat(lang): Add Italian language
refactor!: Drop support for Node 6
```

## The PR title and its merge commit message

When a `release` is created ([see: Release the power of your code! - Make a Release](release-flow.md)), **GitHub** automatically generate the changelog using the `pull requests` titles.  
Although the same rules apply as for commits, it is preferable to omit the `type` in the title creation. This will make the changelog more suitable for the layman.

`GitHub` uses a default merge commit message, like: `Merge pull request #123 from username/branch-name`.
Obviously, no one will ever guess what this commit does by reading this kind of title.  
To improve the git history readability of the project, also use (copy) the PR title as the merge commit message but adding, at the end, the `PR` reference.

> Recently GitHub added an option that does this automagically for us: _In your repo > Settings > Pull Requests > Select Allow merge commits (pre selected) > Select "Default to pull request title"_

The result:

`Add conventional commits paragraph (PR #5)`

will turn the git log in a _readable **story**_.

## So, why use Conventional Commits?

- Automatically determining a semantic version bump (based on the types of commits landed). ([see: Versioning](release-flow.md#versioning))
- Communicating the nature of changes to teammates, the public, and other stakeholders.
- Triggering build and publish processes.
- Making it easier for people to contribute to your projects, by allowing them to explore a more structured commit history.
- Automatically generating `CHANGELOGs`.

This (can) save us a lot of work (and thinking).
