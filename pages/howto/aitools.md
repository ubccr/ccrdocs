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


## Coding Agents

Coding agents are programs that combine LLMs that can reason with tools that let the model act. They allow users to write code from natural language prompts, a process commonly called "vibe coding."  At CCR, a more useful interpretation is **coding in collaboration with an agent**. You describe the task and its constraints, the model proposes code, commands, tests, or refactors, and then you run, inspect, and verify the result. The model can accelerate the work, but you still decide whether the output is correct and safe to keep. This is especially helpful for multi-step technical tasks where the model can read files, inspect logs, run commands, and iterate.


### Common AI Mistakes on HPC Systems

Be especially skeptical when a model invents `sbatch` or `srun` flags, confuses [login node work](../hpc/clusters.md#login-nodes) with [compute node work](../hpc/clusters.md#compute-nodes), assumes `pip install` is always the right choice on a shared system (more on that [here](../howto/python.md)), guesses the wrong [module names or versions](../software/modules.md), mixes up `$HOME`, `$SCRATCH`, and project storage, suggests an [MPI](../hpc/jobs.md#mpi) launch pattern that does not match your code, or assumes GPU access without the right [Slurm constraints](../hpc/jobs.md#slurm-directives-partitions-qos). These are common failure modes, not rare edge cases.


### Slurm and Module Advice Needs Verification

When an agent suggests changes to a CCR job, check whether the queue or QOS is valid, whether the node counts and GPU counts are consistent, whether the account is correct, whether the module names are real on this system, whether the launch command matches the application model, and whether the file system path is appropriate for the workload. If the model cannot answer those questions from real local context, it is guessing.  You may point the model to any of [CCR's support documentation](https://docs.ccr.buffalo.edu) and [published examples](https://github.com/ubccr/ccr-examples) to provide center-specific information while also asking it to look at other online resources to help expand your work.  


## Security and Privacy Considerations

When using external AI services, **do not paste credentials, tokens, or private keys into prompts**. Be careful with unpublished or sensitive research data, avoid unrestricted command execution in unsafe environments, and be cautious with third-party plugins, tools, and MCP servers. If you would not paste something into an external service manually, do not hand it to an agent by default.


## Restricting File System Access

Coding agents act on your behalf and have the same permissions that you do on CCR systems. Selecting a project directory does not necessarily prevent access to your home directory, which may contain API keys, SSH configuration, and other secrets.

You should not allow a coding agent to do anything on CCR systems that you yourself would not do. In most cases, you can launch the agent from a login node and let it run small programs as needed for, e.g., debugging, but you should not allow it to run long or resource-intensive jobs directly on the login node.

Because users have access to shared files and data, we recommend using workspace-write mode for vibe coding on CCR's systems. The idea is to have the files you want the agent to manipulate inside a working directory that it has write access to, and any data or files you don't want it to modify or delete are outside the working directory. Most agents default to workspace-write mode, so all you have to do is launch the agent from inside the working directory. If the agent you are using does not use workspace-write mode by default, you can change it in its config file.

We recommend using working directories located in your `$HOME` directory. If the files you want to manipulate are in your group's `/projects` directory, you should copy them to a fresh working directory in `$HOME`. Agents in workspace-write mode have read access everywhere you do, so they can read files in `/projects` that you have access to for necessary context, but cannot make changes there without your permission. It is best practice to use version control in the working directory and commit often while vibe coding.

This strategy relies on workspace-write permissions to safeguard against malicious or erroneous agent behavior. Avoid `full access` and test what is actually blocked. For stronger isolation, use an operating-system sandbox, container, or virtual machine that exposes only the required project directories.  If you want to safely run without approval prompts in full-access mode, you can use a [container-based sandbox](../howto/containerization.md) that has network access disabled and read-only mounts to data and files in `/projects` needed for context.


## CCR Recommendations  

CCR staff are actively exploring tools and connecting with other HPC centers to develop best practices for our shared environments.  This page will be updated as these resources become available. In the meantime, users should treat general-purpose LLM and coding-agent advice as a starting point, and validate all commands, configurations, and results against CCR documentation and their own workflow requirements.


### References 

Thanks to [NERSC](https://www.nersc.gov/) for their excellent documentation, of which most of this page is built off of.

We highly recommend reviewing the Harvard Kempner Institute's "[Using Agentic AI on the Cluster](https://handbook.eng.kempnerinstitute.harvard.edu/s5b_agentic_ai_workflows/using_agentic_ai_on_the_cluster.html)" documentation for more details and examples.