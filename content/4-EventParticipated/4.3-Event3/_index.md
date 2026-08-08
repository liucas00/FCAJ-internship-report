---
title: "Event 3: AWS FCAJ Agent Forge - Deep Dive Day 2"
date: 2026-08-08
weight: 3
chapter: false
pre: " <b> 4.3. </b> "
---

## Event Information

- **Event:** AWS FIRST CLOUD AI JOURNEY - AGENT FORGE DEEP DIVE
- **Time:** 09:00 AM - 12:00 PM, Saturday, August 8, 2026
- **Location:** 26th Floor, Bitexco Financial Tower
- **Speakers:** Nghia Tran – Agentic SA; Pham – Cloud Consultant, G-AsiaPacific Vietnam
- **Role:** Participant

## Event Overview

Agent Forge Deep Dive Day 2 focused on the practical and architectural aspects of building production-ready AI Agent systems with Amazon Bedrock AgentCore.

The session was divided into two main parts. The first part covered the core AgentCore concepts, including Memory, Evaluations, and Observability. The second part was a hands-on lab where participants worked directly with the available tools in an AWS environment.

This format made it easier to connect the technical concepts from the presentation with their practical use in an Agent development workflow.

## AgentCore Memory

One of the main topics of the session was the memory architecture behind an AI Agent.

AgentCore Memory is organized into two major areas: **Short-term Memory (STM)** and **Long-term Memory (LTM)**. These two areas are connected through an **Automatic Memory Extraction Module**, allowing the system to process and retain information according to its intended use.

### Short-term Memory

**Short-term Memory (STM)** handles information that is relevant to the current session.

It includes:

- **Chat Messages:** the actual content exchanged between the user and the Agent.
- **Session State:** information describing the current state of the interaction.

STM also supports **Branching**, which allows an interaction to follow different conversation or processing paths while preserving the original context.

This can be useful when a user wants to revise an earlier message or take the conversation in a different direction without losing the previous flow.

### Long-term Memory

**Long-term Memory (LTM)** is designed for information that remains useful beyond the current session.

The session introduced several memory strategies.

#### Summary

The Summary strategy creates a condensed representation of important interaction content and results.

Instead of repeatedly relying on the entire conversation history, the Agent can work with a shorter representation that preserves the information that matters.

#### User Preferences

User Preferences allow the system to retain recurring user preferences and behavioral patterns.

This is particularly useful for applications that require personalization. Information learned from previous interactions can be used to make future responses more relevant to a specific user.

#### Semantic & Episodic Memory

Semantic & Episodic Memory helps retain domain-specific knowledge as well as decisions and events from previous interactions.

These stored experiences can then provide useful context for later processing and help improve the Agent's performance across interactions.

## Namespaces and Metadata

AgentCore Memory also provides **Namespaces** and **Metadata** to organize long-term memory.

### Namespaces

Namespaces are used to group and isolate memory within a logical structure.

They can be organized hierarchically and can include identifiers such as:

- `{actorId}`
- `{strategyId}`

This approach is useful when an application needs to manage memory for multiple users, actors, or strategies while keeping their data within separate logical scopes.

### Metadata

While Namespaces define the logical scope and isolation of stored information, **Metadata** provides additional information within that namespace.

Metadata keys can be indexed to support **pre-filtering** before a query is performed.

Together, Namespaces and Metadata provide a more structured way to organize memory and control the scope of information that an Agent can retrieve.

## Hands-on Lab

After the architecture session, participants moved to the **Hands-on Lab**, guided by Pham.

The practical session took place directly in an AWS Lab environment, allowing participants to work with the tools instead of only following demonstrations.

The main activities included:

- Configuring **Add memory** to provide memory capabilities and support more personalized AI behavior.
- Using **AgentCore Evaluations** to monitor and evaluate Agent performance.
- Exploring **Observability** to inspect the Agent's processing flow.
- Working with **Harness** tools within the AgentCore ecosystem.

The lab provided a practical view of how Memory, Evaluations, and Observability can work together during the development and monitoring of an AI Agent.

## Experience and Key Takeaways

What I found most useful about the event was the combination of technical concepts and hands-on practice.

The session gave me a clearer understanding of how memory should be designed for a modern AI Agent. Separating **Short-term Memory** from **Long-term Memory** allows the Agent to handle current-session information differently from information that needs to remain available for future interactions.

The use of **Namespaces** also showed how memory can be organized into separate logical scopes. This becomes especially important when an Agent needs to work with information belonging to different users or strategies.

The hands-on section reinforced the concepts from the presentation. Working directly with Memory, Evaluations, and Observability made their roles in a production-ready Agent architecture easier to understand.

## Applying the Knowledge to the Cloud Finance Platform

The concepts introduced during AWS FCAJ Agent Forge can be applied directly to the **Cloud Finance Platform**, especially the AI-powered personal finance assistant.

### Personalizing the Financial Assistant

The **User Preferences** strategy in Long-term Memory could allow the financial assistant to remember recurring spending patterns and preferences for individual users.

For example, if a user repeatedly demonstrates certain spending habits, the Agent could retain those patterns and use them during future conversations.

This would allow the assistant to provide responses based not only on the current question but also on relevant information learned from previous interactions.

### Data Separation and Security

**Namespaces**, combined with identifiers such as `{actorId}`, can provide logical isolation between different users.

This is particularly important for the Cloud Finance Platform because transaction history and conversation context may contain personal financial information.

Organizing memory by user-specific scopes can reduce the risk of an Agent retrieving information belonging to another user and provides a clearer structure for managing stored data.

## Conclusion

AWS FCAJ Agent Forge - Deep Dive Day 2 gave me a deeper understanding of memory and context management for AI Agents using Amazon Bedrock AgentCore.

The three areas that stood out most were **Memory, Evaluations, and Observability**. Within the Memory architecture, STM, LTM, Namespaces, and Metadata provide the foundation for organizing and retaining information in a controlled way.

These concepts can be applied to the development of the Cloud Finance Platform, particularly for building a personalized financial assistant and maintaining clear separation between users' data.

## Event Photos

![AWS FCAJ Agent Forge - Deep Dive Day 2](https://vvinh118.github.io/fcaj-workshop/4-eventparticipated/4.3-event3/event3.jpg)