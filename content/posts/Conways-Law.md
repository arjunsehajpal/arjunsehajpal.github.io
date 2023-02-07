+++ 
draft = false
date = 2022-12-11T00:38:16+05:30
title = "Conway’s Law: How much influence does it really carry?"
description = ""
slug = ""
tags = ["Product-Management"]
categories = []
externalLink = ""
series = []
+++
Software design is an iterative process. Its longevity depends upon thousands of small design decisions taken every day, and each decision should be in sync with the other. This constant attention to detail is what makes a software system tick. Hence, the quality of software depends hugely on the efficiency of communication between humans building it. This observation became the basis of Conway’s Law.

Paraphrasing Dr. Melvin E. Conway, “Any organization that designs a system, will produce a design whose structure is a copy of the organization’s communication structure.” Though Dr. Conway used the term “system” in context to System Theory, where everything is a system and everything is a part of a system. And it is certainly true for software systems. Conway’s law is an observational law, which tries to build a connection between innovation and the impact and working methodologies and structure of the organization. A classic example of this law would be Apple’s iOS and Android, with the former being a closed in-house project and the latter being developed by open-source contributors all over the globe. This difference is quite obvious as iOS despite being very efficient, doesn’t gel well with others. On the other hand, Android is more flexible but isn’t as well organized as its counterpart.

## Degree of susceptibility
As it is an observational law, its impact on the final shape of software isn’t quantifiable. That being said, a new project generally is much more susceptible to this law, but only as much as the flexibility of the design allows. Also, the projects which have grown considerably, and have their design cemented, and are much less influenced by Conway’s Law. In this sense, the degree of susceptibility to Conway’s Law becomes a function of the flexibility available.

It has been also observed that the teams that are organized on the basis of activities they perform (i.e. separate teams for UI, Testing, and Backend) are more prone to the effects of Conway’s Law. Organizations tend to create teams on the basis of specialization in favor of the belief that this promotes skill-sharing and development and maximum utilization of the personnel. But this separation disregards the interplay each layer of the software has amongst them. In theory, it shouldn’t be too hard for different teams to communicate and collaborate, but in practice, these artificial boundaries do add some friction.

## Inverse Conway Maneuver
As we now understand what this Law is, the next organic step is to understand how we respond to it. The first two ways are obvious, we can either reject its existence or embrace it wholeheartedly. The latter is superior to the former, where we can take steps to ascertain that communication patterns don’t act as a blocker to the realization of the software architecture we envisioned. But in recent years, there has been a rise in the third way to respond to Conway’s Law, where teams are reorganized deliberately, which encourages desired software architecture. This is known as Inverse Conway Maneuver.

The advocates of the Inverse Conway Maneuver live by the commandment that “to get a better system design, all we have to do is to reorganize the team structure.” While their belief is worthy of respect, it won’t always solve the problem. As we have seen above, rigid systems which have lost their flexibility aren’t much susceptible to Conway’s Law and “just” reorganization won’t change anything  (if anything, it would make things worse). So, if the system is still in a nascent state, and is flexible, applying Inverse Conway Maneuver can yield good results, otherwise it is better to peel off the software layer by layer and redesign as per the requirements.

## Conway’s Law and agile
Software systems are a reflection of the people building them and the prior beliefs they have about the software. These beliefs when shared become models and architectures. For the development of good products, it becomes increasingly important that these models and architectures don’t sit in developers' or architects’ minds but are thoroughly documented in form of UML diagrams and Wikis. It becomes better when these models are evolved with strict adherence to a design approach. So, a product benefits from open communication, aligned goals, and fast decisions. Hence, Conway’s Law can be considered as an argument in favour of agile. 

## Conclusion
Though organization structures can influence the design of our software systems, this relationship should be considered nothing more than a constraint. The first aim should always be to keep the flexibility of our systems intact because there is no alternative to a good design. And if we have in our hands a rigid system, organization restructuring should go hand-in-hand with system redesign. Conway’s Law can only be an aide, it’s not a remedy for poor design.
