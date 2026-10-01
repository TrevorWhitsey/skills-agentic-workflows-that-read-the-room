---
name: update-github-info
on:
  schedule: daily
  workflow_dispatch:

permissions:
  contents: read

engine: copilot

tools:
  web-fetch: {}
  edit: {}

network:
  allowed:
    - github.blog
    - github.com
    - awesome-copilot.github.com

safe-outputs:
  create-pull-request:
    title-prefix: "[github-info] "
    reviewers: [mona]
    draft: false
    max: 1
---

# Update GitHub Info

Read `notes/mona-notes.md` and `site/content/github-info.md` before drafting any changes.

Use the web-fetch tool to read:

- https://github.blog/latest/
- https://github.blog/changelog/
- https://awesome-copilot.github.com/workflows/

Select recent items and workflows that provide practical value to developers. Update `site/content/github-info.md` with concise, factual summaries that fit Mona's editorial angle. Cite the relevant GitHub Blog, Changelog, or Awesome Copilot source link for every new item. Do not invent details or rewrite unrelated sections; leave the file unchanged if there is no worthwhile update.

When you make a meaningful update, propose only the resulting content change through the configured create-pull-request safe output. Open one non-draft pull request and request Mona (`mona`) as reviewer. Include this short diagnostic line in the pull request description: `DEBUG: Mona's source scan has landed.` Never write changes directly to the default branch.