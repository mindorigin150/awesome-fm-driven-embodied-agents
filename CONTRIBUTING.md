# Contributing

Suggest a project or correction through an issue or pull request. Include a primary source and explain how the work fits this list.

## Scope

Include systems where a general-purpose foundation model participates in embodied planning, tool use, action selection, execution feedback, or agent improvement. Include evaluation resources that assess such agents.

Language models, vision-language models, and systems that use VLAs as execution components can all fit. Simulation and real-robot work can both fit.

Standalone models, datasets, and general simulators belong in supporting links when they explain an included system.

## README format

Keep the homepage concise: one bullet per project, with its name, a short title or description, and linked badges. Use the same format in both sections.

```markdown
- <a id="project-name"></a>**Project Name**: Short title or description. [![Code: GitHub](https://img.shields.io/badge/Code-GitHub-2ea44f?style=flat-square)](OFFICIAL_REPOSITORY_URL)
```

- Sort entries alphabetically within each section.
- Preserve existing anchors so other documents can link to entries.
- Use green `Code | GitHub`, red `arXiv | PAPER_ID`, and blue `Website | Project` or `Docs | Guide` badges.
- Add badges only for resources that exist. A paper is optional.
- Keep comparisons, scope explanations, release caveats, and detailed analysis outside the README.

## Sources and comparisons

Use official repositories, documentation, and papers for technical claims. Write descriptions in your own words.

[Comparison notes](comparisons/harnesses.md) cover the model's role, action interface, and feedback mechanisms. Update the relevant row when adding a harness. Link each row to its README entry.

Distinguish released functionality, reported experiments, demonstrations, and planned features. Use `Not documented` when the source does not establish a comparison field. Missing documentation does not establish that a capability is absent.

Date source checks in the comparison notes. For a partial update, date the affected entry. Attribute results to their source and state explicitly if you reproduced them.

## Extend the list

Add new projects to an existing section when it fits. Add a section when several relevant entries need a distinct organizing question.

Create a topic note when there is a concrete comparison to explain. Link to the README entries. Keep project facts in Markdown and avoid empty topic files.

## Before submitting

1. Check the scope, source support, and alphabetical order.
2. Check badge images, link destinations, and unique anchors.
3. Preview the README on GitHub.

Contributions use [CC0-1.0](LICENSE). Linked projects retain their own licenses.
