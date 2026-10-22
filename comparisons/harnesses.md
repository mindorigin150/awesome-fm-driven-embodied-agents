# Harness and Evaluation Notes

[Back to the list](../README.md)

## Harness Comparison

**Sources checked: 2026-10-20.** This table summarizes the official sources linked in the [project directory](../README.md#agent-harnesses). It compares design choices, not performance. We have not reproduced these systems.

| Project | Foundation model's role | Action interface | Feedback and improvement |
| --- | --- | --- | --- |
| [Open Gemini Robot Harness](../README.md#open-gemini-robot-harness) | Gemini plans from calibrated images with coordinate overlays and measured arm state | Restricted skill programs call per-arm primitives and parallel actions. The execution layer converts coordinates and solves inverse kinematics | Human review or `gap_guard` checks each motion segment. Rejection reasons and fresh observations support replanning. Holding checks support handover verification |
| [SenseNova-RoboRSI](../README.md#sensenova-roborsi) | Uses configured prompts, context, skills, and tools in a shared runtime | VLA skills, scripted actions, or end-effector tools | Traces and task feedback guide harness revisions; candidates are retested with model parameters fixed in the harness-improvement workflow |
| [HexaShell](../README.md#hexashell) | A VLM coding agent controls the robot; a second agent diagnoses failures and repairs tools | The `robo` command and Python tools use RGB images, camera calibration, and arm state | Failed episodes guide tool edits and retries; tools are frozen for evaluation |
| [ORA](../README.md#ora) | Chooses perception and motion tools using task and robot context | Grasp proposals and motion planning, checked by a supervisor; no VLA in the reported setup | Observations and action receipts return to the agent; requests and actions are recorded |
| [RoboRSI](../README.md#roborsi) | Splits task management, planning, execution, and review across agents | Executable plans and hierarchical robot skills | Reviewer diagnoses failures; proposed skill changes undergo regression checks before retention |
| [Show-Harness](../README.md#show-harness) | Selects semantic action units from visual observations | Discrete actions translated by an interpreter for each robot | Plugins provide action history and failure recovery; demonstration fine-tuning is a separate operating mode |
| [Embodied Harness](../README.md#embodied-harness) | Calls semantic perception and robot tools | Observation, object localization, proprioception, and grasp tools backed by replaceable providers | Tool outcomes and durable session events; recorded fixtures and live execution are distinct modes |
| [RPent](../README.md#rpent) | Plans and steers execution using memory | VLA manipulation primitives through robot services | Interaction and reflection support memory-guided execution; exploration can produce task memory |
| [ASPIRE](../README.md#aspire) | Writes and refines robot control programs through a coding agent | Executable programs call perception, planning, grasping, and control primitives | Multimodal execution traces support failure diagnosis, repair, and validation; validated fixes become reusable skills, with evolutionary search over programs |

Open Gemini Robot Harness is a third-party implementation of Google's published harness design, extended to two arms. Its [repository](https://github.com/ehehee/open-gemini-robot-harness) documents human approval of each motion segment in all recorded real-robot case-study runs. The automatic checker is validated in simulation and scripted checks. Recorded real-robot validation remains future work. The [author's case study](https://ehehee.github.io/blog/open-gemini-harness/) reports development runs with changing prompts and harnesses, rather than a controlled success-rate benchmark. Sources checked: 2026-10-23.

HexaShell's [paper](https://arxiv.org/abs/2610.23479) describes the acting and optimizer agents. Its [repository](https://github.com/HexaFuture/HexaShell) releases frozen tools, interfaces, and evaluation results. The full harness and evolution loop are not included. Sources checked: 2026-10-21.

ASPIRE's [official method description](https://research.nvidia.com/labs/gear/aspire/#method) documents its execution engine, skill library, and evolutionary search. Source checked: 2026-10-20.

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

## Entry Dates

Entries use the arXiv v1 submission date when a paper exists. Otherwise, they use the first official release or launch record below. Dates were checked on 2026-10-20.

| Project | Date | Source |
| --- | --- | --- |
| Open Gemini Robot Harness | 2026-10-20 | [Author's launch post](https://ehehee.github.io/blog/open-gemini-harness/), checked 2026-10-23 |
| SenseNova-RoboRSI | 2026-10-16 | [Initial code release announcement](https://github.com/OpenSenseNova/SenseNova-RoboRSI#news) |
| HexaShell | 2026-10-16 | [arXiv v1 submission history](https://arxiv.org/abs/2610.23479), checked 2026-10-21 |
| ORA | 2026-10-15 | [Release announcement](https://github.com/hao-ai-lab/ORA#news) |
| RoboRSI | 2026-10-08 | [arXiv v1 submission history](https://arxiv.org/abs/2610.12424) |
| Show-Harness | 2026-09-09 | [arXiv v1 submission history](https://arxiv.org/abs/2609.10522) |
| Embodied Harness | 2026-08-24 | [Author's launch post](https://yanming03.github.io/content/blogs/embodied-harness/) |
| RPent | 2026-07-09 | [Harness VLA arXiv v1 submission history](https://arxiv.org/abs/2607.08448) |
| ASPIRE | 2026-06-30 | [arXiv v1 submission history](https://arxiv.org/abs/2607.00272) |
| Embodied First Exam | 2026-10-19 | [Release announcement](https://github.com/mll-lab-nu/embodied-first-exam#news) |
| Robo Use | 2026-09-21 | [First PyPI release, 0.0.1](https://pypi.org/project/robouse/0.0.1/) |
