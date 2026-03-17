---
description: LangChain Prompt Engineering & Workflow Guidelines
---

# LangChain & Prompt Engineering Guidelines

This document outlines best practices for Prompt Engineering and using LangChain concepts within the Darom project.

## 1. Prompt Engineering Best Practices

### The Inverted Pyramid (Journalistic Style)
For news generation, strictly adhere to the Inverted Pyramid structure:

1.  **The Lead (Most Important)**: Who, what, when, where, why, and how. The reader should get the core story in the first paragraph.
2.  **The Body (Crucial Details)**: Argument, controversy, story, specific details, evidence, and quotes.
3.  **The Tail (Extra Info)**: Interesting related facts, background context.

### Chain of Thought (CoT)
Encourage the model to "think" before answering.
- *Example*: "Before generating the article, outline the key facts in order of importance."

### Few-Shot Prompting
Provide examples of the desired output format and style.
- *Example*: "Here is an example of a good Lead Paragraph: [Example]..."

### Delimiters & Structure
Use clear delimiters to separate instructions from data.
- Use `---` or `"""` to wrap context chunks.
- Use Markdown headers for different sections of the prompt.

## 2. LangChain Workflows

### Sequential Chains
Break complex tasks into sequential steps.
- **Step 1**: Research/Gather Context (Context Gatherer).
- **Step 2**: Outline/Plan (Optional implementation).
- **Step 3**: Draft Content (Generator).
- **Step 4**: Critique/Refine (Optional review step).

### Agents vs. Chains
- **Chains**: Hardcoded sequence of steps (Reliable, faster). Use for standard article generation.
- **Agents**: AI decides which tools to use. Use for complex research tasks (e.g., "Find the latest news on X, calculate the growth rate, and write a summary").

## 3. Implementation in Darom

- **Prompt Manager**: Centralize all prompts in `infrastructure/external_services/prompt_manager.py`.
- **Context Handling**: Ensure all dynamic context (hashtags, timeframes) is injected safely.
- **Persona Injection**: Always define the "Who" (e.g., "You are an expert AI Journalist").
