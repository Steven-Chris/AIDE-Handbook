Part I — Foundations
Chapter 1: The Mindset Shift

How software development used to work
What changes when AI enters the workflow
The dangerous middle ground: using AI without a framework
The central principle, introduced in full
Why understanding what you ship is non-negotiable

Chapter 2: Understanding AI Models

What an AI coding assistant actually is (and isn't)
How LLMs generate code — from prompt to output, under the hood
How your prompt, codebase context, and model knowledge combine to produce code
Why understanding this pipeline makes you a better AI user
Model capabilities, limitations, and failure modes
Hallucinations: what they are, why they happen, how to consistently identify them, how to rectify them, and how to reduce their frequency
Choosing the right model for the right task (model agnostic, Claude as primary example)
When NOT to use AI

Chapter 3: Tokens — The Fundamental Unit

What a token is, from first principles
How tokenisation works under the hood
The context window: what it means and why it matters
How token count affects output quality, cost, and reliability
Token optimisation strategies (input and output)
Managing long conversations: when to continue vs. start fresh
Context window management for large codebases
Introduction to tools (e.g. token counters, context formatters)
Prompting implications: writing token-efficient, high-quality prompts


Part II — Setup & Environment
Chapter 4: Your AI Development Environment

Principles of a good AI-assisted dev setup
IDE integrations and when to use them
CLI-based AI tools (Claude Code and equivalents)
Connecting AI to your ecosystem: MCP servers, GitHub, Jira, docs
Custom instructions and persistent context (CLAUDE.md and equivalents)
Environment for juniors vs. seniors (what to add as you grow)

Chapter 5: Prompt Engineering for Engineers

Why prompting is a skill, not a trick
Anatomy of a good engineering prompt
Giving AI the right context: codebase, constraints, conventions
Prompting for different tasks: features, bugs, tests, refactors, docs
Common prompting mistakes and how to fix them
Building reusable prompt templates / skills
Junior vs. senior prompting patterns


Part III — The AI-Assisted SDLC
Chapter 6: Planning with AI

Using AI to break down features and requirements
Generating and stress-testing technical specifications
Architecture and system design: AI as a sounding board
Evaluating tech choices and tradeoffs with AI
What AI cannot plan for you — and why that matters
Prompts and workflows for planning

Chapter 7: Coding with AI

The central principle in practice: solve first, then implement
Translating your solution into effective AI instructions
Incremental implementation: why small, scoped prompts win
Reading, understanding, and validating AI-generated code
When to reject AI output entirely
Handling hallucinated APIs, packages, and patterns
Junior patterns vs. senior patterns for AI-assisted coding

Chapter 8: Testing with AI

AI-assisted test generation: what it's good at and where it falls short
Writing prompts that produce meaningful tests (not just coverage theatre)
Using AI to identify edge cases you missed
TDD with AI: test-first workflows
Reviewing AI-generated tests — the traps to watch for
Junior vs. senior testing patterns

Chapter 9: Refactoring with AI

When and why to use AI for refactoring
Giving AI enough context to refactor safely
Avoiding scope creep in AI refactors
Validating refactored code: it still has to make sense to you
Large-scale vs. surgical refactors

Chapter 10: Documenting with AI

Where AI genuinely excels: documentation
Generating inline comments, docstrings, READMEs, ADRs, changelogs
Keeping documentation honest: AI will document what the code does, not what it should do
PR descriptions, commit messages, and release notes
Building a documentation workflow into your AI habits


Part IV — Team & Process
Chapter 11: AI in Team Workflows

How AI changes code review dynamics
Onboarding new engineers with AI
Shared prompt libraries and team conventions
AI transparency in the workplace: removing the stigma, why honesty about AI usage makes teams stronger not weaker, and how to communicate it clearly in PRs, reviews, and conversations
Avoiding AI-introduced inconsistency across a codebase

Chapter 12: Security, Privacy & IP

The risk of pasting proprietary code into AI tools
What gets sent, what gets stored, and what that means
Safe practices for using AI with sensitive codebases
AI-generated code and intellectual property considerations
Evaluating AI tools for enterprise security compliance


Part V — Staying Sharp
Chapter 13: Avoiding the Crutch

The slow erosion of engineering fundamentals
How to use AI and still keep growing as an engineer
Deliberate practice in an AI-assisted world
Knowing when to go back to first principles
Junior engineers: what you must learn yourself before leaning on AI

Chapter 14: Evaluating & Evolving Your AI Workflow

How to know if your AI workflow is actually working
Measuring quality, not just speed
Iterating on your prompts, tools, and habits over time
Staying current as models and tooling evolve rapidly
Building a feedback loop into your practice
