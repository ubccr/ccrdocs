# AI Coding Tools

This page collects practical guidance for using large language models (LLMs) and coding agents as part of a CCR workflow.  Large language model (LLM) agents are developing rapidly, so the practices in this section are not necessarily the best or final approaches. We will update our recommendations here frequently so please check back often. An agent’s configuration does not make it safe by itself: remain present, review proposed actions, and follow the precautions below.


!!! warning "Practical Advice Only"
    The guidance on this page is provided with the goal of preventing users from running processes that degrade the user experience for others. It should not be construed as a complete policy for AI usage at CCR. CCR is in the process of developing a more detailed policy around AI usage and access to CCR by coding agents that aligns with
    [CCR's Appropriate Use Policy](../policies/misuse.md).  Refer to the [AI Tools & Use Policy](../policies/aipolicies.md) for current policy information and contact [CCR Help](../help.md) if you have questions, concerns, or suggestions.

AI coding tools should be used to reduce repetitive work while keeping humans in control of correctness, performance, and security. **As stated in the [current policy](../policies/aipolicies.md), models must not be permitted to operate unsupervised.**

!!! danger "Scope and Responsibility"
    Users may use coding agents as user-directed development assistants for authorized CCR project work. Users remain responsible for all prompts, commands, code, data access and modification, resource usage, software installation, and external network activity performed by or through the agent. Use of coding agents must conform to [CCR's AI Tools & Use Policy](../policies/aipolicies.md). Agents must not be given prohibited data, must not bypass access controls, and must not perform security testing, prohibited software use, or activity
    outside the approved scope of your research project.  This document provides **general guidance**, not guarantees about correctness, security, performance, or resource usage. Users are responsible for **validating generated code, commands, configurations, and scientific results** before using them in production or allocating large computing resources.


**LLMs can produce incorrect or misleading outputs, including inefficient job configurations, invalid scientific conclusions, or unsafe commands. Over-reliance on generated output without sufficient technical understanding may also reduce visibility into system behavior and degrade overall code or workflow quality.**


## What Are Coding Agents?

Coding agents are programs that combine LLMs that can reason with tools that let the model act. They allow users to write code from natural language prompts, a process commonly called "vibe coding."  At CCR, a more useful interpretation is **coding in collaboration with an agent**. You describe the task and its constraints, the model proposes code, commands, tests, or refactors, and then you run, inspect, and verify the result. The model can accelerate the work, but you still decide whether the output is correct and safe to keep. This is especially helpful for multi-step technical tasks where the model can read files, inspect logs, run commands, and iterate.


### When They Help

Coding agents are often useful when the task is concrete, repetitive, and easy to validate. At CCR that often means:

* drafting or improving [Slurm job scripts](../hpc/jobs.md)
* explaining failures from `sacct`, `squeue`, or log output
* translating shell workflows into Python
* cleaning up notebooks and analysis scripts
* writing README files and usage examples
* refactoring small utilities into more maintainable code

These tasks benefit from rapid iteration and clear feedback loops.

### When To Be Careful

Coding agents are much less reliable when performance is critical and the code has not been benchmarked, when the model is guessing about MPI, GPU, or file system behavior, or when the request depends on exact CCR policy or system behavior that was never provided in context. You should also use extra caution for anything involving credentials, tokens, sensitive research data, allocations, or production workflows. In those cases, the cost of a plausible but wrong answer is much higher.

### Why CLI Agents Are Often a Good Fit

For CCR work, command-line agents are often a better fit than pure chat interfaces because they can inspect repositories directly, read configuration files and logs, run shell commands, suggest or apply small patches, and work naturally with version control. This fits common CCR workflows, which already depend heavily on the shell, job scripts, and text-based tooling.


### Prompting That Works

A good prompt usually names the target system, such as the UB-HPC cluster, explains the exact goal, points to the relevant files, includes the current script or configuration, and provides representative stderr, logs, or job output. It should also define what success looks like. In practice, it helps to ask for the smallest viable patch, explicit assumptions, ranked debugging hypotheses, and clear verification steps.

#### Weak Prompt

> Help me run my code on CCR.

#### Strong Prompt

> I am running a Python MPI workflow on the UB-HPC cluster. Here is my Slurm script, module list, output and error logs. The job hangs after initialization. Propose the smallest script changes to improve launch reliability and explain why.


### Examples of Using an AI agent at CCR:

**Creating batch scripts:**  
You might ask an AI agent for assistance creating a batch script for use at CCR.  An agent can help write this, but you still need to verify that the account and QOS are valid, that the requested resources match the workload, that the module setup is correct, that the launch pattern matches the application, and that the output path is appropriate for the workflow.  For more background, see [Running Jobs](../hpc/jobs.md) and [CCR's Example Repository](https://github.com/ubccr/ccr-examples), which you can also point your AI agent to!


**Troubleshooting job problems:**  
The model is often more useful when you give it evidence instead of a vague description.  For example:
```
login$ sacct -j [YourJobID] --format=JobID,JobName,Partition,Account,AllocTRES%40,Nodelist,State,ExitCode,Elapsed
```
A strong follow-up prompt would be:

> Here is the `sacct` output for my failed job on CCR's UB-HPC cluster and my batch script. Explain what the state and exit code suggest, then propose the next two debugging steps.

That is much more actionable than "my job failed."  Hint: this information is also extra helpful when contacting [CCR help](../help.md) for assistance!  


## Common AI Mistakes on HPC Systems

Be especially skeptical when a model invents `sbatch` or `srun` flags, confuses [login node work](../hpc/clusters.md#login-nodes) with [compute node work](../hpc/clusters.md#compute-nodes), assumes `pip install` is always the right choice on a shared system (more on that [here](../howto/python.md)), guesses the wrong [module names or versions](../software/modules.md), mixes up `$HOME`, `$SCRATCH`, and project storage, suggests an [MPI](../hpc/jobs.md#mpi) launch pattern that does not match your code, or assumes GPU access without the right [Slurm constraints](../hpc/jobs.md#slurm-directives-partitions-qos). These are common failure modes, not rare edge cases.


### Slurm and Module Advice Needs Verification

When an agent suggests changes to a CCR job, check whether the queue or QOS is valid, whether the node counts and GPU counts are consistent, whether the account is correct, whether the module names are real on this system, whether the launch command matches the application model, and whether the file system path is appropriate for the workload. If the model cannot answer those questions from real local context, it is guessing.


## Good Engineering Makes Agents Better

Coding agents work better when your workflow is already disciplined. Breaking larger tasks into smaller steps, using Git commits between working states, running linters, compilers, and tests, and giving the model checks it can run itself all make the agent more reliable. It also helps to keep each session focused on one problem at a time. If the model can inspect the result, it can often help repair its own mistakes.

The same idea applies to multi-agent work. If you ask several helpers to work in parallel, you still need clear task boundaries, a sensible integration plan, and a human review step before combining their output. Parallelism can improve throughput, but it does not remove the need for judgment.


### Context Engineering

The less irrelevant context you include, the better the model usually performs. Useful habits include writing `AGENTS.md` or similar project instructions, documenting project structure and build steps, mentioning cluster-specific assumptions explicitly, and starting fresh sessions when switching tasks.

For example, you may point the model to any of [CCR's support documentation](https://docs.ccr.buffalo.edu) and [published examples](https://github.com/ubccr/ccr-examples) to provide center-specific information while also asking it to look at other online resources to help expand your work.  


## Security and Privacy Considerations

When using external AI services, **do not paste credentials, tokens, or private keys into prompts**. Be careful with unpublished or sensitive research data, avoid unrestricted command execution in unsafe environments, and be cautious with third-party plugins, tools, and MCP servers. If you would not paste something into an external service manually, do not hand it to an agent by default.


## Restricting File System Access

Coding agents act on your behalf and have the same permissions that you do on CCR systems. Selecting a project directory does not necessarily prevent access to your home directory, which may contain API keys, SSH configuration, and other secrets.

You should not allow a coding agent to do anything on CCR systems that you yourself would not do. In most cases, you can launch the agent from a login node and let it run small programs as needed for, e.g., debugging, but you should not allow it to run long or resource-intensive jobs directly on the login node.

Because users have access to shared files and data, we recommend using workspace-write mode for vibe coding on CCR's systems. The idea is to have the files you want the agent to manipulate inside a working directory that it has write access to, and any data or files you don't want it to modify or delete are outside the working directory. Most agents default to workspace-write mode, so all you have to do is launch the agent from inside the working directory. If the agent you are using does not use workspace-write mode by default, you can change it in its config file.

We recommend using working directories located in your `$HOME` directory. If the files you want to manipulate are in your group's `/projects` directory, you should copy them to a fresh working directory in `$HOME`. Agents in workspace-write mode have read access everywhere you do, so they can read files in `/projects` that you have access to for necessary context, but cannot make changes there without your permission. It is best practice to use version control in the working directory and commit often while vibe coding.

This strategy relies on workspace-write permissions to safeguard against malicious or erroneous agent behavior. Avoid `full access` and test what is actually blocked. For stronger isolation, use an operating-system sandbox, container, or virtual machine that exposes only the required project directories.  If you want to safely run without approval prompts in full-access mode, you can use a [container-based sandbox](../howto/containerization.md) that has network access disabled and read-only mounts to data and files in `/projects` needed for context.


## CCR Recommendations  

CCR staff are actively exploring additional guidance and reusable agent configurations for common HPC workflows, including project-specific `SKILL.md` files, agent guidance files for Claude and Codex, prompt templates, and examples for working with Slurm, modules, and job logs.  This page will be updated as these resources become available. In the meantime, users should treat general-purpose LLM and coding-agent advice as a starting point, and validate all commands, configurations, and results against CCR documentation and their own workflow requirements.


### References 

Thanks to [NERSC](https://www.nersc.gov/) for their excellent documentation, of which most of this page is built off of.