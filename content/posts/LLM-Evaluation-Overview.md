+++ 
draft = false
date = 2023-11-08T00:38:16+05:30
title = "LLM Evaluation 01: Overview"
description = ""
slug = ""
tags = ["LLMOps"]
categories = []
externalLink = ""
series = []
+++

LLMs have been all the rage now. Whether you believe in the potential of LLMs or you are still in the camp of sceptics, it doesn’t matter. It’s the stakeholders’ opinion about LLMs that matters. This is because LLMs make it quite easy to “wow the users” and attract them to the product. So, they facilitate onboarding new users to the product. However, it is the trust that retains the users. And, as most of us know by now, LLMs make numerous mistakes. As the complexity rises and users receive incorrect answers frequently, they won’t trust the system and will revert to the tools they were using before.

This post is my attempt to consolidate the research around LLM evaluation and come up with a loose framework that enhances the trustworthiness of LLM-powered applications.

## 1. Why traditional evaluation framework won’t work?
When we developed Machine Learning models in the pre-LLM era (BC can now be Before ChatGPT), we had a precise checklist which formed our evaluation framework. We divided our input dataset into training, evaluation and test sets and measured the performance by calculating metrics on these datasets.

{{< figure src="/blog-img/06-traditional-evaluation-framework.jpg" title="Fig 1: Traditional Evaluation Framework" >}}

But this same approach doesn’t work for LLMs. This is because the traditional approach is based on two key pillars, i.e.,  data and metrics. As LLMs are expensive to train, most applications resort to calling an external API, provided by the OpenAIs and Anthropics of this world. And, good luck with getting the data for these models. But even if one has trained their own LLM (hence, they have data), the question that looks us in the eyes is “what metrics to calculate for evaluation?”. The output of LLMs are more on the qualitative side and are hard to quantify. Another challenge is General-Purpose nature of LLMs. They can perform a diverse set of behaviours. Thus, aggregate metrics become more or less inefficient.

To summarise, there are three challenges in evaluating the LLMs:
- Access to training data
- Qualitative outputs, which are hard to quantify
- Diversity of behaviour

## 2. Makeshift evaluation framework for LLMs
As discussed in the previous section, traditional evaluation strategy needed a dataset and a bunch of metrics to calculate on that dataset. So, building on this, we will divide our approach into two steps:
- What dataset to use?
- What metrics to measure?

### 2.1. Evaluation dataset
A dataset is any set of records. As opposed to the supervised paradigm of model training, we don’t have input-output pairs to begin with. So, we will have to compile our own data. To do so, we can follow the following three-step strategy.

#### 2.1.1. Look out for interesting cases
The best way to prepare the dataset is to just **start**. Accumulate the ad hoc prompts that you use. For instance, write a short paragraph about ``subject``. Here, the subject could be anything, from an inanimate object to a pet.</br>
As you are firing these prompts, there will be some unique and interesting cases where the LLM will fail to generate the “required” output and will require some tweaks in the prompt. You can consolidate these *tricky*, *hard* and *unique* examples into a small dataset.

#### 2.1.2. Incrementally add more data
As the LLM application is rolled out, we can start capturing the real time feedback from the users. This feedback could be handled in two ways:
- *Explicit feedback*: this sort of feedback is easier to capture. Here, we just ask the user whether he liked the answer generated or not. As OpenAI does, we can provide a thumbs-up and thumbs-down icon to collect this type of feedback.
- *Implicit feedback*: as opposed to explicit feedback, this feedback is relatively difficult to collect. One way to collect implicit feedback is to check if the user is asking the same question (different words but semantically having the similar meaning)  multiple times.

{{< figure src="/blog-img/06-chatgpt-explicit-feedback.png" title="Fig 2: Explicit Feedback in ChatGPT" >}}

Using explicit and implicit feedback, we can collect cases which users disliked the output for and add them to data created in the previous step. Also, we can look out for underrepresented topics, intents and documents (in other words, edge cases).



