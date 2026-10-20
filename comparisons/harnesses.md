# Harness and Evaluation Notes

[Back to the list](../README.md)

## Harness Comparison

**Sources checked: 2026-10-20.** This table summarizes the official sources linked in the [project directory](../README.md#agent-harnesses). It compares design choices, not performance. We have not reproduced these systems.

| Project | Foundation model's role | Action interface | Feedback and improvement |
| --- | --- | --- | --- |
| [Embodied Harness](../README.md#embodied-harness) | Calls semantic perception and robot tools | Observation, object localization, proprioception, and grasp tools backed by replaceable providers | Tool outcomes and durable session events; recorded fixtures and live execution are distinct modes |
| [ORA](../README.md#ora) | Chooses perception and motion tools using task and robot context | Grasp proposals and motion planning, checked by a supervisor; no VLA in the reported setup | Observations and action receipts return to the agent; requests and actions are recorded |
| [RoboRSI](../README.md#roborsi) | Splits task management, planning, execution, and review across agents | Executable plans and hierarchical robot skills | Reviewer diagnoses failures; proposed skill changes undergo regression checks before retention |
| [RPent](../README.md#rpent) | Plans and steers execution using memory | VLA manipulation primitives through robot services | Interaction and reflection support memory-guided execution; exploration can produce task memory |
| [SenseNova-RoboRSI](../README.md#sensenova-roborsi) | Uses configured prompts, context, skills, and tools in a shared runtime | VLA skills, scripted actions, or end-effector tools | Traces and task feedback guide harness revisions; candidates are retested with model parameters fixed in the harness-improvement workflow |
| [Show-Harness](../README.md#show-harness) | Selects semantic action units from visual observations | Discrete actions translated by an interpreter for each robot | Plugins provide action history and failure recovery; demonstration fine-tuning is a separate operating mode |

Capability descriptions do not imply that every backend or experiment is publicly released. For example, SenseNova-RoboRSI's [BenchZoo table](https://github.com/OpenSenseNova/SenseNova-RoboRSI#benchzoo) distinguishes released integrations from planned ones.

## Evaluation Notes

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
