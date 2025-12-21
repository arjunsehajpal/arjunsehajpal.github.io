+++ 
draft = false
date = 2025-12-21T01:19:02+05:30
title = "Spec-driven Development"
description = "Antidote to crisis of vibe-coding"
slug = ""
authors = []
tags = ["Software Development Practices"]
categories = []
externalLink = ""
series = []
+++

The emergence of AI coding agents has fundamentally transformed how the software is developed. They’re no longer a novelty, but a legitimate part of a developer’s toolkit. Though early coding assistants like GitHub Copilot were only able to generate small code snippets and perform completions, as LLMs improved and the context window grew larger, it became easier to generate software directly from natural language instructions. This gave rise to vibe-coding. </br>
Vibe-coding is great for greenfield use cases, prototyping and creative exploration, but is not equally performant on the existing codebases and legacy systems. This is because vibe-coding treats software development as a series of isolated interactions. This unstructured chain of interactions where one describes a goal, prompts the LLM and repeats until the code “feels right”, has led to proliferation of anti-patterns and code smells.</br>
To overcome this, we need a coherent process that reasserts the primacy of structured thinking and intentional design. One of the software industry’s more rigorous answers to fill this gap is Spec-driven development (SDD).</br>

# Philosophy
For years, software development has treated code as a protagonist, with spec being a scaffolding that is built and discarded once the real work begins. Spec-driven development inverts this relationship as spec becomes the executable blueprint that directly generates the working implementation. Still in its nascent years, the definition of SDD is in flux. But the core idea is simple: instead of prompting a model with “build authentication”, which forces a coding agent to assume many unstated requirements, the spec provides it with more clarity and improves overall efficiency.</br>
At the centre of SDD is a spec, which is a contract detailing how code should behave. A spec is a well-crafted software requirement artifact, which an agent can use to generate code.</br>
Because it is behaviour-oriented, a spec should be written in a language that clearly expresses software functionality and can guide AI coding agents. It often takes the form of GIVEN/WHEN/THEN scenarios. It should cover the critical paths without enumerating every possible edge cases. The spec’s primary job is to aim for clarity and sufficient completeness, but it should be the developer's job to steer the direction, and verify the final code.</br>

{{< notice info >}} 
#### Spec-driven Development vs Context Engineering
To provide more context about the code to a coding agent, files such as `agents.md` are added. It structures the information provided to the coding agent, defining roles, rules and capabilities to curate project context and help the agent perform consistently. But it is not a substitute for the SDD as it doesn’t specify the intended behaviour. So, in other words, despite adding files such as `agents.md` or `projects.md`, the code generation will largely remain emergent, with structure as well as intent inferred implicitly rather than defined upfront.</br>
In practice, SDD and context engineering should be treated as complementary, where the former captures the intended behaviour of the system, while the latter establishes the operating environment for the agent.
{{< /notice >}}

# Practice
As discussed earlier, the practice of spec-driven development is still evolving, and there is no single, canonical workflow that defines it. In practice, however, three broad implementation levels tend to emerge across teams adopting SDD. These levels differ in how central the spec is to the development process and how tightly it is coupled to code generation, and represent increasing levels of reliance on the spec as a durable artifact. The three commonly observed paradigms are:</br>
1. <u>Spec-first</u>: a well thought-out spec is written first and then used by the agent to generate code.
2. <u>Spec-anchored</u>: similar to spec-first, but the spec is maintained even after code is generated, to support future evolution and maintenance of the feature.
3. <u>Spec-as-source</u>: the spec is the primary source of truth, maintained by the developer. The developer doesn’t directly edit the code, treating it as a derived artifact.

The above three paradigms mostly differ in how the spec document is maintained and how authoritative it is relative to the code. All these paradigms treat the spec as a central guiding document, not an afterthought. If maintained correctly, the spec becomes a living document that not only captures functional and non-functional requirements, but also the requirements around security policies, compliance requirements, system constraints and integration needs.</br>
The positive side-effect of maintaining a spec is that it becomes easy to track these organization-wide policies. Rather than being captured in some obscure wiki, these policies become tightly integrated with the code itself.

## Workflow
Spec-driven development follows a structured workflow that typically progresses through four stages: specify, plan, task, and implement. Each of these stages produces an artifact that serves as an input to subsequent phases, creating a coherent development progression.

### Stage 01: Specify
The process begins with the “specify” stage, where the developer provides a high-level description of the goal. This description may be succinct, for instance, “create a multi-step user registration flow with email verification” or more elaborate. The goal here is to focus on the functional requirement, user needs, and business objectives. </br>
For a more detailed specification, the developer can include user journeys, and what “success” looks like. A useful way to approach this is by answering a small set of framing questions:
1. Who is the user?
2. What problem does this feature solve?
3. How does the user interact with this feature?

These questions mark the starting point, failure conditions, boundary conditions and definition of “done”. Once these are in place, developers can engage with the agent to craft a well-defined spec document. The output is a functional specification. Tools like GitHub’s [Spec-Kit](https://github.com/github/spec-kit) use the `/specify` command to initiate this interactive drafting session. 

### Stage 02: Plan
Once the specifications are approved, the Plan phase translates these into a technical implementation strategy. This is where the developers make the architectural decisions and define constraints. This document outlines:
- **Technology stack**: document technology choices and their rationales. For instance, “we will use PostgreSQL for ACID compliance and strong performance on the anticipated query patterns.”
- **Architectural patterns**: document architectural patterns. For instance, “implement a REST API with layered architecture: controllers handle HTTP requests, services handle business logic, and models handle data models. Dependencies between layers are managed via dependency injection to ensure loose coupling.”
- **Implementation standards**: document language-specific standards. For instance, “`async/await` for asynchronous tasks.”
- **Security and compliance specifications**: non-functional requirements are documented explicitly. For instance, “sensitive data is encrypted at rest using AES-256.”

In addition, this stage may also define data contracts and testing approaches.</br>
This plan is crucial from the perspective of context engineering. Using this specification, the agent grounds itself in the project’s architecture, significantly reducing hallucinations. 

### Stage 03: Task
The task phase takes the plan and decomposes it into small, atomic, and discrete actionable items that can be executed sequentially or in parallel. This phase is critical for maintaining developer momentum and enabling clear progress tracking. The output of this stage is a task list that serves as a stable execution plan for the coding agent.</br>
This decomposition resembles agile planning practices, but operates within the shorter execution–feedback cycles of LLM-driven development. Explicit task boundaries help prevent agents from oscillating between concerns or revisiting previously completed work.</br>
A practical guideline at this stage is to size individual tasks so they can be completed by the agent in a single, focused session. Tasks that are too large risk context overflow, while tasks that are too small introduce unnecessary context switching and coordination overhead.

### Stage 04: Implementation
In the final stage, the coding agent implements tasks according to the defined task list. As code is generated, it is continuously validated against the specification through tests and explicit checks. Automated tests derived from acceptance criteria run immediately, providing feedback on whether the implementation matches the intended behaviour. </br>
The developer’s role at this stage is to review the output against the spec. If the implementation fails verification, the spec is updated or clarified, and the agent is guided to revise the implementation. This creates a tight feedback loop in which the spec and the software evolve together. </br>
As the agent encounters errors, these errors and their resolutions can be recorded in a “lessons learned” section of the spec. Over time, this forms a lightweight knowledge base that can be surfaced to the agent in future iterations to help avoid repeating similar issues.

# Considerations and Challenges
Spec-driven development has shown considerable promise, especially in zero-to-one use cases, where an entirely new application is built from scratch or a proof of concept is developed. These are also the scenarios where vibe-coding typically excels. However, the most significant impact I have observed from SDD is in N to N+1 use cases, where a new feature is added to an existing application. In such scenarios, developers can scan the codebase and accompanying documentation to generate a sufficiently detailed spec, enabling the implementation of features that remain consistent with the system’s existing architecture.</br>
While I have not directly worked on large-scale brownfield modernization efforts, where legacy systems are refactored or re-architected, SDD appears promising even in this context. Capturing the essential business logic of a legacy system in a spec can enable the development of new functionality without inheriting existing technical debt.</br>
That said, SDD is not without challenges. One of the primary issues today is the lack of consensus on what constitutes a “good” spec. Projects such as [Kiro](https://kiro.dev/) and [Spec-Kit](https://github.com/github/spec-kit) are actively exploring this space, but the ecosystem is still early, and best practices are far from standardized.</br>
Another fundamental challenge stems from the nature of LLMs themselves. LLMs are inherently non-deterministic, and regardless of how detailed or well-crafted a spec is, code generation cannot be assumed to be fully reproducible. While this may be acceptable during initial development, it poses meaningful challenges during upgrades, debugging, and long-term maintenance.</br>
Finally, SDD must contend with the broader industry problem of documentation decay. Without active maintenance, specs risk becoming outdated as the code evolves. If specifications are not updated alongside implementation changes, inaccuracies accumulate, ultimately reducing the spec’s effectiveness as a guiding artifact.

# Conclusion
The emergence of spec-driven development reflects the maturation of AI-assisted software development from creative experimentation toward a more disciplined engineering practice. By explicitly separating planning from implementation, SDD addresses many of the structural shortcomings of vibe-coding while preserving the productivity gains offered by coding agents. <br>
While the term itself may not capture public attention in the same way as vibe-coding, the underlying ideas point to a more sustainable path forward. As coding agents become more deeply embedded in real-world software systems, practices that emphasize clarity, intent, and verification are likely to matter far more than novelty.
