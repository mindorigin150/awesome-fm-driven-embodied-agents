# Contributing

Help this list explain how foundation models become embodied agents. Contributions can add relevant work, correct facts, or clarify differences between systems.

## What belongs here

A harness entry should show how a general-purpose foundation model participates in embodied planning, tool use, action selection, execution feedback, or agent improvement. Include a primary source that describes the system.

An evaluation entry should explain how tasks or evaluation infrastructure assess such agents. State what the agent can observe, how it acts, and how the evaluator determines success when the sources document these details.

Language models, VLMs, and systems that use VLAs as execution components can all fit. Simulation and real-robot work can both fit.

Standalone models, datasets, and general simulators belong in supporting links when they explain an included system. Keep the main directory focused on the agent and its interaction with the environment.

## Add or update a project

1. Check the existing entries for the project or a previous name.
2. Read its official repository, documentation, or paper.
3. Add a concise entry in alphabetical order.
4. Give the entry a stable, lowercase HTML anchor.
5. Add or update its comparison row if it is a harness.
6. Check links, anchors, and the Markdown preview.
7. Open a pull request that explains the addition or correction and cites its sources.

An issue is also welcome when you want to propose a project before editing the list.

### Harness entry

Use this format, replacing the placeholders:

```markdown
<a id="project-name"></a>

- **[Project Name](OFFICIAL_REPOSITORY_URL)** — Explain the model's role and the mechanism that connects it to robot execution. [Documentation](OFFICIAL_DOCS_URL) · [Paper](PAPER_URL).
```

Keep the description to two or three short sentences. Include only links that exist. A paper is optional.

The comparison row should cover:

- **Foundation model's role:** The decisions or operations the model performs.
- **Action interface:** The commands, tools, skills, or policies through which it acts.
- **Feedback and improvement:** The observations or execution results it receives, and any documented adaptation mechanism.

Link the comparison row to the canonical entry. Do not copy the full project description into the table.

### Evaluation entry

Use a stable anchor and a project heading. Add a short overview, followed by three bullets:

- **Interface:** How an agent interacts with the task.
- **Evaluation:** How the system records or scores execution.
- **Sources:** Official repository, documentation, and protocol links where available.

Distinguish tasks, evaluation infrastructure, and simulators. A project can provide more than one of these.

## Evidence and wording

- Use primary sources for technical claims.
- Write descriptions in your own words.
- Describe mechanisms rather than repeating promotional claims.
- Distinguish released functionality, reported experiments, demonstrations, and planned features.
- Use `Not documented` when the source does not establish a comparison field.
- Do not treat missing documentation as evidence that a capability is absent.
- Do not describe a partial demonstration as a completed task.
- Attribute reported results to their source. State explicitly if you reproduced them.
- Avoid rankings across different task sets or evaluation protocols.

Keep the comparison date accurate. When checking the entire group, update its date. For a partial update, add a date and source to the affected row or entry.

If you add numerical results, provide the model, tasks, protocol, and source. Include relevant budgets, retries, memory, human assistance, and learning conditions. The initial directory deliberately omits a performance leaderboard.

## Extend the structure

Use the existing sections when they fit. Propose a new section when several relevant entries need a distinct organizing question.

Add a topic note when it answers a concrete question through sourced comparisons. Link to canonical project entries and keep detailed analysis outside the README. Do not create empty topic files.

Keep project facts in Markdown. Add structured data or generation tools only when a concrete maintenance need justifies them.

## Before submitting

- Confirm that the contribution fits the scope.
- Check that each technical claim has a supporting source.
- Check alphabetical order and unique project anchors.
- Check local links and external destinations.
- Preview tables and navigation on GitHub.

Contributions to this list use [CC0-1.0](LICENSE). Do not copy third-party figures, logos, or long passages into the repository.
