+++ 
author = "Arjun Sehajpal"
title = "Monitoring the Machine Learning System"
date = "2023-05-26"
description = "A detailed introduction to Model Calibration"
tags = [
    "MLOPs"
]
+++
Almost every Machine Learning pipeline starts from the raw data and ends at decisions. Any amount of bad data can lead to faulty decisions, which could further lead to loss of business (and in some cases, organisation’s reputation). As the data pipelines grow more and more complex, it becomes increasingly important to have a robust monitoring and observability structure in place. Neglecting this component results in monitoring debt, which is paid back in Developer’s time.

# Monitoring Debt
Analogous to technical debt, monitoring debt represents the gap between the monitoring ideals and monitoring reality. Much like technical debt, where we factor how the cost of redesigning and refactoring tomorrow allows us to ship the code today, in monitoring debt, a team gives up the ability to catch issues ahead well ahead of the stakeholders to release fast. But not enough time is not the only issue that the code becomes indebted, it can also be due to incompetence.

Like financial debt, monitoring debt can be a good thing. But repaying monitoring debt (or technical debt of any kind) is difficult. And, it usually boils down to two scenarios:
1. Will the same developers be around to pay the debt?
2. If they are not, does the new developer have the documentation to acquire the intimate knowledge of the codebase? This must include:
    - What behaviour is normal?
    - What are high-priority events one should monitor for?

It is best to have **yes** as an answer to the first scenario, because if the old developers didn’t have time to put proper monitoring and logging in place, you can’t expect much from documentation either.

If one doesn’t want to end up in these scenarios, it is best to embrace the three truths about monitoring.
1. <u>Monitoring is high-skilled activity</u> - As stated above, to enable monitoring in a system requires one to have clear knowledge of monitoring goals and monitoring mechanism. The former requires in-depth knowledge of the functioning of the system to be monitored, while the latter requires knowledge of how to instrument the system.
