# Awesome Foundation-Model-Driven Embodied Agents

**From Foundation Models to Physical Agents: Harnesses, Interfaces, and Evaluation.**

A curated research map of how general-purpose foundation models become embodied agents, starting with **embodied agent harnesses**.

The central question: **How do foundation models use tools, actions, and feedback to complete tasks in the physical world?**

## Scope

We focus on systems where a foundation model takes an active role in planning, tool use, action selection, feedback-based correction, or agent improvement. Tasks can run on real robots or in simulation.

An **embodied harness** connects a model to observations, action interfaces, execution, and feedback. It can also manage context, memory, tools, and evaluation. The model may act through code, semantic actions, robot skills, or a vision-language-action model (VLA).

The starting point is the recent group of harness projects below. The scope includes language models and vision-language models (VLMs), with VLA-based execution where relevant. Standalone models, datasets, and general simulators appear as supporting links when they help explain a listed system.

## Contents

- [Agent Harnesses](#agent-harnesses)
- [Harness Comparison](#harness-comparison)
- [Evaluation & Environments](#evaluation--environments)
- [How This Map Grows](#how-this-map-grows)
- [Contributing](#contributing)
- [License](#license)

## Agent Harnesses

Projects are listed alphabetically. Each entry is the canonical reference for that project within this list.

<a id="embodied-harness"></a>

- **[Embodied Harness](https://github.com/imakiyui/embodied-harness)** — Extends DeepSeek Harness with semantic tools for RGB observation, object localization, proprioception, and grasp execution. Replaceable providers connect the same agent to recorded fixtures or a live RoboTwin process. The documented live demo shows grasp and lift, with full task completion unclaimed. [Architecture](https://github.com/imakiyui/embodied-harness/blob/HEAD/docs/architecture.md).

<a id="ora"></a>

- **[ORA](https://github.com/hao-ai-lab/ORA)** — Uses open-weight language models to call perception, grasp, and motion-planning tools. A supervisor checks and dispatches actions. The reported setup uses no VLA, robot training, or task-specific memory. [Method and results](https://haoailab.com/blogs/ora/).

<a id="roborsi"></a>

- **[RoboRSI](https://github.com/nssmd/RoboRSI)** — Organizes robot self-improvement around Manager, Planner, Engineer, and Reviewer agents. A task–skill tree supports exploration, code consolidation, and revision of skills after failures. [Paper](https://arxiv.org/abs/2610.12424) · [Project](https://lab.noematrix.ai/blog/2-roborsi/).

<a id="rpent"></a>

- **[RPent](https://github.com/RLinf/RPent)** — Combines an agentic planner, memory, and robot execution services. Its Harness VLA work uses memory-guided agents to steer frozen VLAs as manipulation primitives. [Documentation](https://rpent.readthedocs.io/en/latest/) · [Paper](https://arxiv.org/abs/2607.08448).

<a id="sensenova-roborsi"></a>

- **[SenseNova-RoboRSI](https://github.com/OpenSenseNova/SenseNova-RoboRSI)** — Connects models, skills, tools, and evaluation through a shared runtime. Its recursive self-improvement workflow uses execution traces to revise the harness and retest candidate changes. This is a separate project from nssmd/RoboRSI. [Documentation](https://github.com/OpenSenseNova/SenseNova-RoboRSI/blob/main/docs/README.md).

<a id="show-harness"></a>

- **[Show-Harness](https://github.com/showlab/Show-Harness)** — Lets a VLM select discrete semantic actions that robot-specific interpreters translate into motion. It supports both zero-shot frontier VLMs and smaller VLMs fine-tuned on demonstrations. [Project](https://showlab.github.io/Show-Harness/) · [Paper](https://arxiv.org/abs/2609.10522).

## Harness Comparison

**Sources checked: 2026-10-20.** This table summarizes the official sources linked above. It compares design choices, not performance. We have not reproduced these systems.

| Project | Foundation model's role | Action interface | Feedback and improvement |
| --- | --- | --- | --- |
| [Embodied Harness](#embodied-harness) | Calls semantic perception and robot tools | Observation, object localization, proprioception, and grasp tools backed by replaceable providers | Tool outcomes and durable session events; recorded fixtures and live execution are distinct modes |
| [ORA](#ora) | Chooses perception and motion tools using task and robot context | Grasp proposals and motion planning, checked by a supervisor; no VLA in the reported setup | Observations and action receipts return to the agent; requests and actions are recorded |
| [RoboRSI](#roborsi) | Splits task management, planning, execution, and review across agents | Executable plans and hierarchical robot skills | Reviewer diagnoses failures; proposed skill changes undergo regression checks before retention |
| [RPent](#rpent) | Plans and steers execution using memory | VLA manipulation primitives through robot services | Interaction and reflection support memory-guided execution; exploration can produce task memory |
| [SenseNova-RoboRSI](#sensenova-roborsi) | Uses configured prompts, context, skills, and tools in a shared runtime | VLA skills, scripted actions, or end-effector tools | Traces and task feedback guide harness revisions; candidates are retested with model parameters fixed in the harness-improvement workflow |
| [Show-Harness](#show-harness) | Selects semantic action units from visual observations | Discrete actions translated by an interpreter for each robot | Plugins provide action history and failure recovery; demonstration fine-tuning is a separate operating mode |

Capability descriptions do not imply that every backend or experiment is publicly released. For example, SenseNova-RoboRSI's [BenchZoo table](https://github.com/OpenSenseNova/SenseNova-RoboRSI#benchzoo) distinguishes released integrations from planned ones.

## Evaluation & Environments

**Sources checked: 2026-10-20.** These entries focus on evaluation infrastructure for agents. A benchmark supplies tasks and scoring rules. An evaluation harness runs agents against those tasks. A simulator provides the environment.

<a id="embodied-first-exam"></a>

### [Embodied First Exam](https://www.embodied-first-exam.ai/)

Evaluates coding agents on robot tasks drawn from multiple benchmark suites. Agents write programs, run robots, and inspect results in frozen scenes. It runs on Harbor and provides task modes with different observation and execution conditions. Programs are verified in a separate sandbox.

- **Interface:** Code execution within a task environment.
- **Evaluation:** Suite-specific task verification; select the task mode when interpreting results.
- **Sources:** [Repository](https://github.com/mll-lab-nu/embodied-first-exam) · [Running and protocols](https://github.com/mll-lab-nu/embodied-first-exam/blob/main/docs/protocol/running.md).

<a id="robo-use"></a>

### [Robo Use](https://robouse.ai/)

Turns robot benchmarks into tasks that agent harnesses solve through the `robo` shell command. An episode server runs the simulator, enforces the step budget, records execution, and scores the final physical state. It uses BenchFlow task and trial formats.

- **Interface:** Shell commands to a simulator episode server.
- **Evaluation:** Task-specific scoring with video, trajectory, and reward records; tasks include reference solutions and no-op controls.
- **Sources:** [Documentation](https://robouse.ai/docs/) · [Published runs](https://robouse.ai/runs).

When comparing results, check the model, task set, observation access, action interface, and execution budget. Also check retries, persistent memory, human assistance, and whether the system learns during evaluation. Follow the linked protocols for each result.

## How This Map Grows

New projects can join the existing sections without changing the scope. Each project keeps one canonical entry; comparison tables and future topic notes link to that entry.

As the collection develops, related questions can become new sections or focused notes:

- **Action and skill interfaces:** How do code, semantic actions, skills, and VLA steering connect models to robots?
- **Execution and adaptation:** How do agents use memory, recover from failures, and improve through interaction?
- **Evaluation protocols:** What do task conditions and execution budgets let us conclude about an agent?

We add a section when there is relevant material to organize. We add a focused note when there is a concrete comparison to explain.

## Contributing

Suggest a project, correct a description, or improve a comparison through an issue or pull request. Include a primary source and explain how the work fits this scope.

See [CONTRIBUTING.md](CONTRIBUTING.md) for entry formats and review criteria.

## License

This list is dedicated to the public domain under [CC0-1.0](LICENSE). Linked projects retain their own licenses.
