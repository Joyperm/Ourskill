---
name: our-prompting
description: Write effective prompts for LLMs — named frameworks (RTF, CO-STAR, RISE, APE, CRAFT, GRADE, etc.), structure, few-shot examples, chain-of-thought, system prompts, and output parsing. Use to construct or refine a prompt, pick a prompting framework for a task, or shape a vague request into a precise prompt.
user-invocable: true
---

# Prompt Engineering

Write prompts that get reliable, high-quality output from LLMs.

## Core Principles

1. **Be specific** — vague prompts get vague results
2. **Show, don't tell** — examples beat instructions
3. **Structure the output** — tell the model exactly what format you want
4. **Iterate** — prompts are code; test and refine them

## Named Frameworks (pick a starting template)

Named frameworks are small **component templates** — pick one that matches the
task, fill each labeled component, and you get a structured prompt. They scaffold
the prompt; the **Techniques** below fill it in.

**How to pick:** classify the task → match the "Best for" column → fill every
component (if one stays empty, drop to a simpler framework).

| Framework | Components | Best for |
| --- | --- | --- |
| **RTF** | Role, Task, Format | Quick single-turn commands |
| **TAG** | Task, Action, Goal | Direct, target-driven tasks |
| **ERA** | Expectation, Role, Action | Fast, results-only answers |
| **CRAFT** | Context, Role, Action, Format, Tone | Everyday productivity |
| **RACE** | Role, Action, Context, Expectation | Professional roleplay / business comms |
| **RISE** | Role, Input, Steps, Expectation | Multi-step workflows, analytical stress-tests |
| **CARE** | Context, Action, Result, Example | Reports/briefs needing strict examples |
| **CO-STAR** | Context, Objective, Style, Tone, Audience, Response | Content, marketing, copywriting |
| **CREATE** | Character, Request, Examples, Adjustments, Type, Extras | Creative / customized output |
| **CLEAR** | Concise, Logical, Explicit, Adaptive, Reflective | Research, prompt refinement, critical thinking |
| **PREP** | Prompt, Role, Explicit instructions, Parameters | Teaching / educational contexts |
| **APE** | Analyze, Plan, Execute | Reasoning, logic, coding (Chain-of-Thought) |
| **TRACE** | Task, Request, Action, Context, Example | Few-shot / example-heavy tasks |
| **CIDI** | Context, Instructions, Details, Input | Technical / data-heavy analysis |
| **GRADE** | Goal, Role, Action, Details, Example | Structured professional blueprints |
| **STAR** | Situation, Task, Appearance, Refine | Format-heavy iterative output |

**Less-obvious components:** Style = writing register vs Tone = emotional register
(CO-STAR) · Adaptive = let the model ask clarifying questions first (CLEAR) ·
Reflective = model self-evaluates its reasoning (CLEAR) · Appearance = visual
layout / markdown (STAR) · Refine = negative constraints, what NOT to do (STAR) ·
Extras = trailing conditions (CREATE).

**Examples**

RTF (quick command):
> Role: Act as a SQL database administrator.
> Task: Write a query returning the top 5 customers by total spend.
> Format: A single SQL code block with inline comments.

CO-STAR (marketing content):
> Context: Launching a premium reusable water bottle for commuters.
> Objective: Write a product-launch social post.
> Style: Professional B2C copywriter. · Tone: Energetic but trustworthy.
> Audience: Eco-conscious urban commuters 25–40.
> Response: Under 150 words, 3 hashtags, one CTA.

> Frameworks and techniques compose: APE maps to **Chain-of-Thought**; CO-STAR's
> Response and RTF's Format map to **Structured Output** (both below).

## Techniques

### System Prompts

Set the model's role and constraints:

```
You are a senior code reviewer. Review the provided code for:
1. Security vulnerabilities
2. Performance issues
3. Readability problems

For each issue found, provide:
- Severity (critical/warning/info)
- Line number
- Description
- Suggested fix

If no issues are found, respond with "No issues found."
```

### Few-Shot Examples

Provide 2-3 examples of input → output:

```
Convert the user's natural language query to a SQL query.

Example 1:
Input: "How many users signed up last month?"
Output: SELECT COUNT(*) FROM users WHERE created_at >= DATE_TRUNC('month', NOW() - INTERVAL '1 month') AND created_at < DATE_TRUNC('month', NOW());

Example 2:
Input: "Show me the top 5 products by revenue"
Output: SELECT p.name, SUM(o.amount) as revenue FROM products p JOIN orders o ON o.product_id = p.id GROUP BY p.name ORDER BY revenue DESC LIMIT 5;

Now convert this query:
Input: "{user_query}"
Output:
```

### Chain-of-Thought

Ask the model to reason step by step:

```
Analyze this error and suggest a fix. Think step by step:
1. What does the error message mean?
2. What could cause this error?
3. What is the most likely root cause given the code context?
4. What is the fix?
```

### Structured Output

Request JSON or a specific format:

```
Respond with a JSON object matching this schema:
{
  "summary": "string - one sentence summary",
  "sentiment": "positive | negative | neutral",
  "key_topics": ["string"],
  "confidence": 0.0-1.0
}
```

### Constraints and Guardrails

```
Rules:
- Only use information from the provided context
- If you don't know the answer, say "I don't know" — do not guess
- Keep responses under 200 words
- Do not include any PII in your response
```

## Patterns for Code

**Code generation:**
```
Write a TypeScript function that {description}.

Requirements:
- {requirement 1}
- {requirement 2}

Use these libraries: {libraries}
Follow this pattern from the codebase: {example}
```

**Code transformation:**
```
Refactor this code to {goal}. Keep the same behavior.
Do not change the public API (function signatures, exports).
```

**Bug fixing:**
```
This code has a bug: {description of bug}

Error: {error message}

Fix the bug. Explain what caused it in a comment.
```

## Anti-Patterns

- **Too vague**: "Make this better" → Be specific about what "better" means
- **Too long**: Giant prompts with everything → Split into focused prompts
- **Contradictory**: "Be concise but thorough" → Pick one or define the tradeoff
- **No examples**: Complex formatting without showing what you want → Add 1-2 examples
- **Prompt injection risk**: Including raw user input without delimiting → Use clear delimiters like `<user_input>...</user_input>`

## Tips

- Temperature 0 for deterministic tasks (code, classification), 0.7+ for creative tasks
- Test prompts with edge cases, not just the happy path
- Version control your prompts — they're as important as code
- Use structured output (JSON) when parsing the response programmatically
- Shorter prompts often outperform longer ones if they're precise enough
