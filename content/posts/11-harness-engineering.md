+++ 
draft = false
date = 2026-08-25T07:16:37+05:30
title = "Harness Engineering: The Rise of ChatGPT Wrapper"
description = ""
slug = ""
authors = []
tags = ["AI Engineering"]
categories = []
externalLink = ""
series = []
+++
The “ChatGPT wrapper” was a much-maligned term of 2023. Any tool or product built on top of frontier LLMs to provide a tailor-made solution for a problem, was dismissed under this moniker. But this product development strategy has resurfaced itself in 2026 under the guise of Harness Engineering, and pretty much changed how the interaction layer between humans and LLMs is perceived. 

The [inflection point](https://simonwillison.net/2026/Jan/4/inflection/) was release agents like OpenClaw and Pi built on top of models like Claude Opus 4.5, when models became intelligent enough to call the correct tools, and harness matured enough to provide them with the correct set of tools and information. 

An LLM by itself is not an agent, it becomes one when we provide it with tools and environment to execute these tools, along with a state, and feedback loops to update this state, and if required, with enforceable constraints. So, *harness is everything except the model*.

{{< figure 
    src="/blog-img/11-Harness-Layers.png" 
    width="500px"
>}}

# Goal of a Harness
The main execution pattern for agents today is ReAct Loop. As agents process the information and generate the actions and iterate over this flow, we need a mechanism that can steer the model in the right direction. Coding Agents have a tendency to replicate the pattern that already exists in the repository, no matter how sophisticated or uneven they are. Full autonomy doesn’t solve this problem, in fact it exaggerates existing issues and introduces novel problems. So, it is best to provide Agents with an environment that has strict boundaries, predictable structure and the required tooling. A well-designed harness increases the probability that the agent gets it right in the first place and if not, provides a feedback loop that self-corrects as many issues as possible.

# What is Harness?
A harness is the logic that determines what information an LLM sees at each step, what data points it stores, what information to retrieve and what context to prevent. Hence, harness is a delivery mechanism for [good context engineering](/posts/07-context-engineering-for-agents/). 
</br>
</br>
Concretely, a harness includes:
1. Prompts (system prompt, skills)
2. MCP Servers and Tools
3. Infrastructure (filesystem, browser)
4. Orchestration logic (subagents spawning, model routing, handoffs)
5. Middleware (context compaction, continuation)

{{< figure 
    src="/blog-img/11-Harness-Components.png" 
    width="800px"
>}}


As illustrated in the diagram above, the only job of the model is to reason and decide. Rest all is handled by the harness.

## Verticals of a Harness
When designing a harness, one should think about three core verticals that constitute a Harness: Security, Interoperability and Observability. 

**Security** constitutes the constraints like privacy and governance. When a Person A uses the agent, it should see only what Person A is authorised to see. So, a security aspect of the Harness ensures that permissions trickle down from the user to the agent. Once this is in place, an audit trial should also capture what all artifacts were accessed by the agent and what all actions were taken. This is important for organisations compliant with standards HIPAA or GDPR. [Masking PII data](https://github.com/arjunsehajpal/redacta) from Frontier models and [Human-in-the-loop approvals](https://docs.langchain.com/oss/python/langchain/human-in-the-loop) could be other additions in this vertical.

**Interoperability** constitutes communication and capability-sharing. Agents are useful if they can access your organization’s data. If one agent is able to query Hive tables, every other agent should be able to connect to this agent to leverage this capability. To accomplish this, org-wide standards should be enforced, which can be part of the harness.

**Observability** constitutes creating a feedback system to improve the agent over time. As agents are non-deterministic in nature, they are bound to fail on certain attempts. Identifying common failure patterns from logs, and understanding what strategies worked, and what could be done to refine tool-selection. This can be enabled by tracing the steps that agent took, logging queries, responses and tool calls, and analyzing all these traces and logs to create a monitoring framework. 


# Designing the Harness
The harness primitives can either be a proactive suggestion or a reactive feedback that agent receives from the action it undertakes. The former aims to steer the agent before it acts, dictating constraints and boundaries and nudging agent towards expected behaviour. These include principles, conventions, how-tos etc. The latter are consumed by an agent after the action has been undertaken. These could be logs or search results.

The other dimension of the harness primitives could either be deterministic or non-deterministic in nature. The deterministic primitives are fast, and reliable. These include Unit Tests, linters, CodeMod engines etc. The non-deterministic primitives are driven by LLM. The results could be a bit unreliable, and driven by prompts and skills provided. 

{{< figure 
    src="/blog-img/11-guides-two-by-two.png" 
    width="800px"
>}}

The best way to design a Harness is to work backwards from the desired agent behaviour. For instance, if an agent needs to do data analysis, it will need access to the filesystem to read data, and a code execution platform to write and execute code.

<div class="centered-table">

| Behaviour | Primitives Required |
| --- | --- |
| Work with real-data | Filesystem |
| Write and execute code safely | Sandbox environment |
| Access knowledge | RAG, web-search |
| Long contexts | Compaction, tool offloading |
| Complete long horizon tasks | Loops |

</div>

As there are many moving parts in the Harness, which parts should be built in-house and which one should be bought. A common framework one can follow here is separate the components view where the product differential lay. For an organisation building something internally, it usually is in the business expertise. This includes, but not limited to, when and what content to surface and how to handle domain-specific edge-cases. The infrastructure to enable this, like sandboxing, authentication, can be bought.

# Conclusion
While the LLMs are important, the orchestration layer around the model (how the context is managed, how retrieval happens, what to store in active memory, and how errors are handled) is where a massive amount of real-world performance also lives. This is pretty freeing for builders as one need not to train an LLM from scratch, but building a great harness for a specific use-case can be a differentiating factor. That's not a bad value proposition for a "ChatGPT wrapper."

