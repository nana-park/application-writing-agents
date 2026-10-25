# Application Writing Agents

Korean-language instructions for a team of agents that research a role, verify experience, write application drafts, and review them.

This repository contains skills and workflow documents. It is not a standalone app or an automatic application submission service.

## HTML research reports and publication

For the Career Workspace HTML site, the private **Application Writer Multi-Agent** repository is the source of truth for company/JD/essay definitions, schemas, templates and renderers. [Job Application Strategist](https://github.com/nana-park/job-application-strategist) publishes approved exports from that writer. This public repository remains a sanitized instruction edition; it is not the HTML renderer or a second source for that site's research policy.

Authorized maintainers use the private writer's validated preparation command, then review and approve the public diff. There is no background synchronization and this repository does not contain the private renderer dependencies. Do not run the writer commands from this checkout or copy private source records here. See [HTML publication boundary](docs/html-publication.md) for the exact division and validation limits.

## Quick start

1. Download or clone the repository and open it in your agent workspace.
2. Use [AGENTS.md](AGENTS.md) as the entry point.
3. Provide the company, role, job description, all questions, word or character limits, and experience sources you allow the agents to use.
4. The main agent coordinates research and planning, evidence checks, A/B drafts, and independent HR and role-specific reviews.
5. Check the facts and final text before submitting an application.

Korean example request:

> AGENTS.md를 읽고 이 JD와 문항에 맞는 지원서 초안을 도와줘. 먼저 필요한 자료와 경험 근거를 확인해줘.

## Workflow

Main → research and prework → evidence → writing coordinator → A/B drafts → independent reviews → final comparison and user choice.

A and B use the same verified facts but different structures. Missing evidence must stay visible; agents should not invent achievements, dates, numbers, or responsibilities.

## Contents

- `agents/`: main, evidence, writing, and review roles
- `docs/`: handoffs, scheduling, writing, storage, and review contracts
- `skills/`: form entry, experience entries, prework, company research, motivation, and experience coaching
- [Source and privacy rules](docs/sources.md)
- [Validation scope](docs/learning-progress.md)

## Tools and setup

Use a runtime with multi-agent tools. Check the model names and call examples in [dispatch](docs/dispatch.md) against your environment. Reading a role file does not run an agent.

Connect Google Docs, Notion, or a browser only when needed. Choose your own private source and output locations. External writes require a request covering that destination and valid access. Without a configured destination, return a local draft and report it as unsaved externally. Final submission needs a separate explicit request.

## Privacy and limits

This clean public edition excludes personal career editing records, real application data, source transcripts, private identifiers, and the original Git history. Examples are generic or synthetic, not a real applicant's history. No executable code was changed; personal document settings were generalized.

The guides are in Korean. A complete application, external storage, and form-entry run has not been validated with this public edition. Models, connectors, and websites may require setup changes. The workflow does not guarantee acceptance or successful submission.

Keep private inputs and outputs outside tracked files. `private/`, `outputs/`, local source settings, and environment files are ignored by Git. Always inspect staged files: .gitignore does not protect already tracked files or change cloud sharing permissions.
