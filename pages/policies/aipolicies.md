# AI Tools & Use Policy

Artificial intelligence tools are increasingly capable of executing commands, modifying files, submitting computational jobs, and making decisions on behalf of users. These capabilities can improve research productivity, but they also introduce risks that differ substantially from those associated with traditional software and machine-learning workloads.

AI agents can take actions that are unintended by the researcher, generate large numbers of processes or jobs, consume resources unexpectedly, modify or delete data, or otherwise adversely affect shared computing infrastructure. Because the behavior of agentic systems may be probabilistic and difficult to reconstruct after an incident, additional safeguards are necessary when these tools interact with CCR's high-performance computing (HPC) systems.

This policy establishes requirements for the use of agentic AI, autonomous workflows, coding assistants, large language models (LLMs), and traditional machine-learning applications on CCR's systems.  AI coding assistants and other generative AI tools are useful on CCR's clusters, but their use must follow [CCR's acceptable use policy](misuse.md), [UB’s Generative AI Guidelines](https://www.buffalo.edu/ubit/policies/policies-standards-guidelines/ubit-guidance/generative-ai.html), [SUNY Systemwide Artificial Intelligence Policy](https://www.suny.edu/sunypp/documents.cfm?doc_id=933), the [New York State ban on DeepSeek AI use](https://www.buffalo.edu/ubit/news/article.host.html/content/shared/www/ubit/news/2026/deepseek-ban.detail.html), and requirements or restrictions from funding agencies (if applicable to your work). In particular, do not paste confidential (L2 and above) data into public AI services.  As a reminder, CCR's systems do NOT support this type of data (refer to the [Protected Status Data Policy](accounts.md#protected-status-data-policy) for more information).  It is the principal investigator's responsibility to be compliant with any requirements made by funding agencies that have awarded them grant funds.  If you require assistance understanding these requirements or have questions on how to remain in compliance with funding agencies, please contact the [UB's Office of Research Security](https://www.buffalo.edu/research/about-ried/our-units/ors.html).


## Policy

- Any agents run on your behalf are your responsibility.  If CCR's policies are violated by an agent running under your account, you will be subject to account termination and, potentially, referral to UB's IT security office, as described in [CCR's Permitted Use & Misuse Policy](misuse.md#misuse-of-systems-and-abuse-of-account)

- AI agents may not independently create, submit, modify, or operate HPC jobs or execute system commands without explicit user approval of the actions being performed.

- Users must maintain meaningful human oversight of agentic AI activity.

- Users must not provide AI agents with credentials in a manner that unnecessarily exposes or transfers control of those credentials. Passwords, private SSH keys, API tokens, and other authentication secrets must not be placed directly into prompts, agent context, or other unprotected AI input.

- Agentic activity that violates these requirements is subject to immediate termination.

- CCR staff may suspend or terminate an AI agent, process, session, or associated HPC job when its behavior creates or reasonably appears likely to create a risk to system availability, performance, security, data integrity, or other users.`


## Guidance  

Refer to the [AI Coding Tools](../howto/aitools.md) how-to guide for additional information on using agentic AI tools on CCR's systems. 


