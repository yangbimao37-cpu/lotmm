---
name: github-publishing
description: Publish the LotMM root project and its api and app projects to public GitHub repositories, with the child projects linked as submodules.
---

# Publish LotMM projects to GitHub

Use this skill when the user asks to publish this workspace's root project and its immediate `api` and `app` projects to GitHub.

## Repository mapping

- `api` → `lotmm-api`
- `app` → `lotmm-app`
- workspace root → `lotmm`, unless the user names another root repository

Resolve the owner from the authenticated GitHub account. Do not include unrelated folders beside the workspace or nested projects that are not part of this mapping.

## Workflow

1. Inspect the workspace root, the `api` and `app` folders, Git status, remotes, and existing history. Preserve file history and local changes; never force-push or replace a remote repository with unrelated history.
2. Before staging, inspect each project's ignore rules and publish candidates. Keep `.env` files, databases, uploads, dependency folders, generated output, and logs out of commits. Scan candidate files and existing history for credentials and personal contact details. Stop before publishing if a likely secret or private data is present, and report the affected path without exposing its value. For unpublished local history, replace a personal author email with the account's GitHub noreply address while preserving commit contents and messages; do not rewrite history already present on a remote without the user's direction.
3. Treat each public repository creation and push as an external change. Proceed only when the user's current request explicitly asks to publish or make these repositories public; this skill does not grant standing permission for later runs.
4. Create the three public GitHub repositories under the authenticated owner, if they do not already exist. Do not initialize empty remotes with starter files. If an existing repository has unrelated history or contents, stop and ask how to proceed rather than overwriting it.
5. Initialize Git only for projects that do not already have a repository. Commit only reviewed, intended files, and keep Git identity configuration local to these repositories when needed.
6. In the root repository, register `api` and `app` as submodules using their GitHub URLs and pin each to the commit being published. Keep the root README clear about cloning with submodules.
7. Push without force, then verify the owner, repository names, public visibility, pushed commit IDs, and root submodule URLs. Report any repository that could not be published.

Do not assume that a connected GitHub plugin also authenticates command-line Git. Use an available authenticated Git or GitHub workflow, and never print or persist credentials.
