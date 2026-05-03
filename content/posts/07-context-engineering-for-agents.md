+++ 
draft = true
date = 2026-05-03T16:29:55+05:30
title = "Context Engineering for Agents"
description = "Thoughts on how to build reliable agents"
slug = ""
authors = []
tags = ["AI Engineering"]
categories = []
externalLink = ""
series = []
+++

When the long context came into being, there was a lot of excitement around them. It killed the excitement around RAG and pumped the hype for MCPs. Of what use is the carefully crafted RAG pipeline to fetch the best document when one can put every document in the context itself. The Frontier Model Labs latched onto the trend. [Grok 4.1 was launched with a 2 million context window](https://x.ai/news/grok-4-1-fast) which made the Gemini 1 million context window look rather ordinary. But these numbers say more about how much text the LLMs can process without breaking. There’s no guarantee that all the context present in such a large window would be actively reasoned. Chroma published a technical report explaining this, naming this phenomenon as [Context Rot](https://www.trychroma.com/research/context-rot). 

{{< figure 
    src="/blog-img/09-Context-Rot.png" 
    title="Performance of LLMs as input length grows"
    attr="(Source: Chroma)"
    attrlink="https://www.trychroma.com/research/context-rot"
    width="500px"
>}}

The situation becomes worse even more when we move to Agentic Systems. 




