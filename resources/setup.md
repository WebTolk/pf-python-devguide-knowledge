---
title: Getting Started
source_url: https://devguide.python.org/getting-started/
source_type: official_documentation
mirrored_at: 2026-10-02T05:37:05+00:00
package: docs.python-devguide
---

# Getting Started

Source: <https://devguide.python.org/getting-started/>

Contributor setup and first steps.

#Getting started¶ (https://devguide.python.org/getting-started/#getting-started)

Quick reference (https://devguide.python.org/getting-started/quick-reference/)

Set up Git (https://devguide.python.org/getting-started/quick-reference/#set-up-git)

Fork and clone the repo (https://devguide.python.org/getting-started/quick-reference/#fork-and-clone-the-repo)

Build Python (https://devguide.python.org/getting-started/quick-reference/#build-python)

Run the tests (https://devguide.python.org/getting-started/quick-reference/#run-the-tests)

Create issues and pull requests (https://devguide.python.org/getting-started/quick-reference/#create-issues-and-pull-requests)

Create issues for nontrivial changes (https://devguide.python.org/getting-started/quick-reference/#create-issues-for-nontrivial-changes)

Create work branches (https://devguide.python.org/getting-started/quick-reference/#create-work-branches)

Document your changes (https://devguide.python.org/getting-started/quick-reference/#document-your-changes)

Create pull requests (https://devguide.python.org/getting-started/quick-reference/#create-pull-requests)

Work on your pull request (https://devguide.python.org/getting-started/quick-reference/#work-on-your-pull-request)

Don’t force-push (https://devguide.python.org/getting-started/quick-reference/#don-t-force-push)

Setup and building (https://devguide.python.org/getting-started/setup-building/)

Install Git (https://devguide.python.org/getting-started/setup-building/#install-git)

Get the source code (https://devguide.python.org/getting-started/setup-building/#get-the-source-code)

Install pre-commit as a Git hook (https://devguide.python.org/getting-started/setup-building/#install-pre-commit-as-a-git-hook)

Compile and build (https://devguide.python.org/getting-started/setup-building/#compile-and-build)

Unix (https://devguide.python.org/getting-started/setup-building/#unix)

Clang (https://devguide.python.org/getting-started/setup-building/#clang)

Optimization (https://devguide.python.org/getting-started/setup-building/#optimization)

Windows (https://devguide.python.org/getting-started/setup-building/#windows)

WASI (https://devguide.python.org/getting-started/setup-building/#wasi)

Emscripten (https://devguide.python.org/getting-started/setup-building/#emscripten)

Android (https://devguide.python.org/getting-started/setup-building/#android)

iOS (https://devguide.python.org/getting-started/setup-building/#ios)

Install dependencies (https://devguide.python.org/getting-started/setup-building/#install-dependencies)

Regenerate `configure` (https://devguide.python.org/getting-started/setup-building/#regenerate-configure)

Regenerate the ABI dump (https://devguide.python.org/getting-started/setup-building/#regenerate-the-abi-dump)

Troubleshoot the build (https://devguide.python.org/getting-started/setup-building/#troubleshoot-the-build)

Avoid recreating auto-generated files (https://devguide.python.org/getting-started/setup-building/#avoid-recreating-auto-generated-files)

Editors and tools (https://devguide.python.org/getting-started/setup-building/#editors-and-tools)

Directory structure (https://devguide.python.org/getting-started/setup-building/#directory-structure)

Using a container (https://devguide.python.org/getting-started/setup-building/#using-a-container)

Contribute using GitHub Codespaces (https://devguide.python.org/getting-started/setup-building/#contribute-using-github-codespaces)

What is GitHub Codespaces? (https://devguide.python.org/getting-started/setup-building/#what-is-github-codespaces)

Create a CPython codespace (https://devguide.python.org/getting-started/setup-building/#create-a-cpython-codespace)

Use Codespaces locally (https://devguide.python.org/getting-started/setup-building/#use-codespaces-locally)

Using the dev container directly (https://devguide.python.org/getting-started/setup-building/#using-the-dev-container-directly)

Using the pre-built container image (https://devguide.python.org/getting-started/setup-building/#using-the-pre-built-container-image)

Building yourself (https://devguide.python.org/getting-started/setup-building/#building-yourself)

Fixing “easy” issues (and beyond) (https://devguide.python.org/getting-started/fixing-issues/)

Git bootcamp and cheat sheet (https://devguide.python.org/getting-started/git-boot-camp/)

Forking CPython GitHub repository (https://devguide.python.org/getting-started/git-boot-camp/#forking-cpython-github-repository)

Cloning a forked CPython repository (https://devguide.python.org/getting-started/git-boot-camp/#cloning-a-forked-cpython-repository)

Configure the remotes (https://devguide.python.org/getting-started/git-boot-camp/#configure-the-remotes)

Listing the remote repositories (https://devguide.python.org/getting-started/git-boot-camp/#listing-the-remote-repositories)

Setting up your name and email address (https://devguide.python.org/getting-started/git-boot-camp/#setting-up-your-name-and-email-address)

Enabling `autocrlf` on Windows (https://devguide.python.org/getting-started/git-boot-camp/#enabling-autocrlf-on-windows)

Creating and switching branches (https://devguide.python.org/getting-started/git-boot-camp/#creating-and-switching-branches)

Deleting branches (https://devguide.python.org/getting-started/git-boot-camp/#deleting-branches)

Renaming branch (https://devguide.python.org/getting-started/git-boot-camp/#renaming-branch)

Staging and committing files (https://devguide.python.org/getting-started/git-boot-camp/#staging-and-committing-files)

Reverting changes (https://devguide.python.org/getting-started/git-boot-camp/#reverting-changes)

Stashing changes (https://devguide.python.org/getting-started/git-boot-camp/#stashing-changes)

Comparing changes (https://devguide.python.org/getting-started/git-boot-camp/#comparing-changes)

Pushing changes (https://devguide.python.org/getting-started/git-boot-camp/#pushing-changes)

Creating a pull request (https://devguide.python.org/getting-started/git-boot-camp/#creating-a-pull-request)

Linking to issues and pull requests (https://devguide.python.org/getting-started/git-boot-camp/#linking-to-issues-and-pull-requests)

Updating your CPython fork (https://devguide.python.org/getting-started/git-boot-camp/#updating-your-cpython-fork)

Applying a patch to Git (https://devguide.python.org/getting-started/git-boot-camp/#applying-a-patch-to-git)

Checking out others’ pull requests (https://devguide.python.org/getting-started/git-boot-camp/#checking-out-others-pull-requests)

Accepting and merging a pull request (https://devguide.python.org/getting-started/git-boot-camp/#accepting-and-merging-a-pull-request)

Cancelling an automatic merge (https://devguide.python.org/getting-started/git-boot-camp/#cancelling-an-automatic-merge)

Backporting merged changes (https://devguide.python.org/getting-started/git-boot-camp/#backporting-merged-changes)

Editing a pull request prior to merging (https://devguide.python.org/getting-started/git-boot-camp/#editing-a-pull-request-prior-to-merging)

GitHub CLI (https://devguide.python.org/getting-started/git-boot-camp/#github-cli)

Git worktree (https://devguide.python.org/getting-started/git-boot-camp/#git-worktree)

Setting up Git worktree (https://devguide.python.org/getting-started/git-boot-camp/#setting-up-git-worktree)

Using Git worktree (https://devguide.python.org/getting-started/git-boot-camp/#using-git-worktree)

Lifecycle of a pull request (https://devguide.python.org/getting-started/pull-request-lifecycle/)

Introduction (https://devguide.python.org/getting-started/pull-request-lifecycle/#introduction)

Step-by-step guide (https://devguide.python.org/getting-started/pull-request-lifecycle/#step-by-step-guide)

Resolving merge conflicts (https://devguide.python.org/getting-started/pull-request-lifecycle/#resolving-merge-conflicts)

Don’t force-push (https://devguide.python.org/getting-started/pull-request-lifecycle/#don-t-force-push)

Making good PRs (https://devguide.python.org/getting-started/pull-request-lifecycle/#making-good-prs)

Updating NEWS and What’s New in Python (https://devguide.python.org/getting-started/pull-request-lifecycle/#updating-news-and-what-s-new-in-python)

Changes that require NEWS entries (https://devguide.python.org/getting-started/pull-request-lifecycle/#changes-that-require-news-entries)

Changes that require “What’s New in Python” entries (https://devguide.python.org/getting-started/pull-request-lifecycle/#changes-that-require-what-s-new-in-python-entries)

How to add a NEWS entry (https://devguide.python.org/getting-started/pull-request-lifecycle/#how-to-add-a-news-entry)

How to write a NEWS entry (https://devguide.python.org/getting-started/pull-request-lifecycle/#how-to-write-a-news-entry)

Copyrights (https://devguide.python.org/getting-started/pull-request-lifecycle/#copyrights)

Typo fixes (https://devguide.python.org/getting-started/pull-request-lifecycle/#typo-fixes)

`patchcheck` (https://devguide.python.org/getting-started/pull-request-lifecycle/#patchcheck)

Making good commits (https://devguide.python.org/getting-started/pull-request-lifecycle/#making-good-commits)

Licensing (https://devguide.python.org/getting-started/pull-request-lifecycle/#licensing)

Why do I need to sign the CLA again? (https://devguide.python.org/getting-started/pull-request-lifecycle/#why-do-i-need-to-sign-the-cla-again)

Submitting (https://devguide.python.org/getting-started/pull-request-lifecycle/#submitting)

Converting an existing patch from b.p.o to GitHub (https://devguide.python.org/getting-started/pull-request-lifecycle/#converting-an-existing-patch-from-b-p-o-to-github)

Reviewing (https://devguide.python.org/getting-started/pull-request-lifecycle/#reviewing)

How to review a pull request (https://devguide.python.org/getting-started/pull-request-lifecycle/#how-to-review-a-pull-request)

Leaving a pull request review on GitHub (https://devguide.python.org/getting-started/pull-request-lifecycle/#leaving-a-pull-request-review-on-github)

Dismissing review from another core team member (https://devguide.python.org/getting-started/pull-request-lifecycle/#dismissing-review-from-another-core-team-member)

Keeping continuous integration green (https://devguide.python.org/getting-started/pull-request-lifecycle/#keeping-continuous-integration-green)

Update branch button (https://devguide.python.org/getting-started/pull-request-lifecycle/#update-branch-button)

Committing/rejecting (https://devguide.python.org/getting-started/pull-request-lifecycle/#committing-rejecting)

Crediting (https://devguide.python.org/getting-started/pull-request-lifecycle/#crediting)

Where to get help (https://devguide.python.org/getting-started/getting-help/)

Discourse (https://devguide.python.org/getting-started/getting-help/#discourse)

Ask #python-dev (https://devguide.python.org/getting-started/getting-help/#ask-python-dev)

Core mentorship (https://devguide.python.org/getting-started/getting-help/#core-mentorship)

File a bug (https://devguide.python.org/getting-started/getting-help/#file-a-bug)

Guidelines for using AI tools (https://devguide.python.org/getting-started/ai-tools/)

Considerations for success (https://devguide.python.org/getting-started/ai-tools/#considerations-for-success)

Acceptable uses (https://devguide.python.org/getting-started/ai-tools/#acceptable-uses)

Unacceptable uses (https://devguide.python.org/getting-started/ai-tools/#unacceptable-uses)
