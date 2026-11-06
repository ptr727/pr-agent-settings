# pr-agent-settings

Qodo's organization-wide configuration for the `ptr727` repositories.

## Purpose

[Qodo][qodo-link] reads a repository named `pr-agent-settings` under an organization or account as that owner's central configuration. It reads `.pr_agent.toml` from this repository's default branch for any repository that carries no `.pr_agent.toml` of its own on its default branch. A repository that carries one uses its own file instead.

A fleet repository chooses which reviewers run, on which branches, and when, in its own `.github/agent-policy.json`. That file is rendered from the [ProjectTemplate][projecttemplate-link] registry, together with the repository's `.coderabbit.yaml` and `.pr_agent.toml`. So the default here covers only a repository that has not received its rendered files yet. It turns automatic feedback off, so it starts no review nobody asked for.

## Status

This repository holds no `.pr_agent.toml` yet. Qodo reads a repository's own file only from its default branch. So a central default with automatic feedback off would silence Qodo wherever a rendered file has not reached `main`. The central file is added once each fleet repository carries its rendered `.pr_agent.toml` on `main`.

## Where the Rules Live

This repository holds configuration only. The rules it serves live in ProjectTemplate:

- [Pull Request Reviewer Reference][reviewer-reference-link] describes each reviewer bot and how its configuration is committed. Its "Review Configuration" section covers the review policy.
- [`spec/agent-policy.schema.json`][agent-policy-schema-link] defines the policy file, and [`spec/agent-policy.default.json`][agent-policy-default-link] is the default a repository inherits where its own file states none.
- [`GOVERNANCE.md`][governance-link] "PR Review Etiquette" governs how a review is requested, triaged, and resolved.
- [Repository Configuration][repo-config-link] describes `repo-config/configure.sh`, which applies each repository's bot settings.

## Changing the Configuration

Change this repository through a pull request, and only alongside the matching change to the ProjectTemplate review policy. A change here alters review behavior across every repository that carries no `.pr_agent.toml` of its own. The [configuration reference][qodo-config-link] names each option.

<!-- External links -->
[projecttemplate-link]: https://github.com/ptr727/ProjectTemplate
[qodo-config-link]: https://qodo-merge-docs.qodo.ai/usage-guide/configuration_options/
[qodo-link]: https://www.qodo.ai

<!-- ProjectTemplate links -->
[agent-policy-default-link]: https://github.com/ptr727/ProjectTemplate/blob/main/spec/agent-policy.default.json
[agent-policy-schema-link]: https://github.com/ptr727/ProjectTemplate/blob/main/spec/agent-policy.schema.json
[governance-link]: https://github.com/ptr727/ProjectTemplate/blob/main/GOVERNANCE.md#pr-review-etiquette
[repo-config-link]: https://github.com/ptr727/ProjectTemplate/blob/main/docs/repo-config.md
[reviewer-reference-link]: https://github.com/ptr727/ProjectTemplate/blob/main/docs/pr-reviewer-reference.md
