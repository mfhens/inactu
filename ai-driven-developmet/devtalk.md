---
marp: true
paginate: true
theme: ./ey-marp-theme.css
author: Markus Friede Hens
---

<script type="module">
  import mermaid from 'https://unpkg.com/mermaid@10/dist/mermaid.esm.min.mjs';
  mermaid.initialize({ startOnLoad: true });
</script>

# *"AI-Driven Software Development: Friend, Foe, or Rubber Duck?"*

---

# Agenda

- Framing: Why this matters
- What is AI-Driven Development?
- Demo: Codex in VS Code
- Do’s & Don’ts (Field Notes)
- Agentic Engineering (Claude Code Flow)
- The Future
- Q&A

---

# Why This Topic?

- AI is now embedded in our developer workflows.
- Developers ≠ replaced, but **augmented**.
- We gain velocity — but must still apply judgment.
- How do we become *good* at AI-driven development?
---

# What is AI-Driven Development?

<div style="display: flex; gap: 2rem;">
  <div style="flex: 1;">

  **Core Concepts:**

  - Foundation models (LLMs) as fuzzy pair programmers
  - **Strength:** Pattern completion, boilerplate, simple algorithms, docstrings, tests
  - **Weakness:** Logical reasoning, architectural decisions, long-range dependencies
  - AI-driven software development != Auto-coding — it's interactive co-creation
  - Models hallucinate: high fluency, low factual grounding

  </div>

  <div style="flex: 1;">
    <div class="mermaid-container">
      <div class="mermaid">
      sequenceDiagram
          participant Dev as Developer
          participant AI as Copilot
          Dev->>AI: Write a function to parse CSV
          AI-->>Dev: Suggests code
          Dev->>AI: Modify to handle edge case
          AI-->>Dev: Updated code
          Dev->>Dev: Validates, tests, integrates
      </div>
    </div>
  </div>
</div>

---

# Live Demo: Codex in VS Code (15 min)

**Goal:** Show both the power and the limitations.

**Demo ideas:**

- Implement a small REST API controller.
- Generate tests.
- Refactor some legacy-looking code.
- Ask it for architectural suggestions (and show where it gets it wrong).
- Use *"Explain this code"* feature.

**Key takeaway:**

> *AI provides velocity, not judgment.*

---

# Dos and Don'ts
<!-- _class: tight-table -->

| ✅ Do                                                                          | ❌ Don't                                                           |
| ----------------------------------------------------------------------------- | ----------------------------------------------------------------- |
| Use AI to **bootstrap boilerplate** code                                      | Expect it to get **architecture right**                           |
| Use **short, incremental prompts**                                            | Dump large multi-paragraph specs and expect coherent output       |
| Think like a **code reviewer**: Always verify AI output                       | Assume correctness — especially on edge cases, concurrency, state |
| Use AI to **refactor and explain unfamiliar code**                            | Trust its explanations without your own understanding             |
| Be very **explicit**: "Do X in Y style with Z library"                        | Leave instructions vague — LLMs hallucinate gaps                  |
| Use AI to write **parameterized tests** and mocks                             | Rely on AI-generated tests as your sole safety net                |
| Use **code context carefully**: provide files, function headers               | Assume AI can infer missing business rules                        |
| Leverage AI for **docstrings, comments, and documentation**                   | Let documentation drift by not validating technical accuracy      |
| Use AI as a **partner, not a servant**: interactive back-and-forth works best | Expect full solutions from single-shot prompts                    |

---

# Bonus Insight

- AI models sometimes **repeat bugs** you just fixed.
- They **prefer happy-path code** unless explicitly told otherwise.
- They may silently **invent APIs** that don't exist.
- Sometimes they confidently propose **logically invalid fixes**.
- They are prone to **state inconsistency** when large context windows are overloaded.

---
> "Treat the model as an eager junior developer. Good at cranking out boilerplate. Bad at nuance. Always needs code review."
---

# Claude-Code-Flow 🧠

### Agentic Engineering in Action

- Multiple Claude agents:
  - Researcher
  - Coder
  - Tester
  - Security Auditor
- Shared memory (CRDT-based)
- Recursive self-improvement
- Parallel task orchestration

---

# Claude Flow Architecture

<div class="mermaid-container">
    <div class="mermaid">
  flowchart TD
      A[Task Input] --> B[Orchestrator]
      B --> C[Memory Bank]
      B --> D[Agents Pool]
      D --> E[Coder Agent]
      D --> F[Tester Agent]
      D --> G[Security Agent]
      E & F & G --> C
      C --> B
      B --> H[Validated Output]
  </div>
</div>

---

# ✅ Do & ❌ Don’t

<!-- _class: tight-table -->

| ✅ Do                                                                                                                                                    | ❌ Don't                                                      |
| ------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------ |
| Use **multi-stage prompts** — break down tasks into clear, atomic steps                                                                                 | Assume one-shot prompts will yield correct results           |
| Treat the model as a **partner of partners** — e.g., use **Claude‑Flow** to spawn and coordinate multiple specialized agents                            | Expect a single AI tool to handle everything flawlessly      |
| Empower agents with specific roles: coder, tester, researcher, security auditor                                                                         | Leave agent roles undefined and hope for the best            |
| Use **shared memory** across agents — Claude‑Flow’s memory bank ensures context and consistency ([github.com][1], [reddit.com][2], [codenotary.com][3]) | Ignore persistence—each prompt loses context and coherence   |
| Build by leveraging **recursive development**: let agents help build their own orchestrator                                                             | Treat the system as static — no continuous improvement loop  |
| Scale to parallel tasks: let a swarm of agents handle complex workflows simultaneously                                                                  | Funnel everything sequentially — underutilizing AI potential |
| Monitor each agent’s progress via dashboards or terminal UIs, inspect logs                                                                              | Stay dark — no visibility means no control                   |
| Be clear about **failure policies**, rollbacks, agent retry logic                                                                                       | Trust agents implicitly — no undo or safe guardrails         |
| Combine advanced agent orchestration (Claude‑Flow) with interactive prompt-based tools (Copilot, Cursor) for complementary strengths                    | Use only one toolchain — risk redundancy or gaps             |

---

# 🧠 The *claude‑code‑flow* Story: Agentic Engineering in Action

- **Multi-agent orchestration**: ruvnet’s repository demonstrates running dozens of Claude-powered agents in parallel (researcher, coder, tester, security‑auditor) — all coordinated via a shared memory bank and orchestrator ([github.com][1]).
- **Recursive development**: As noted on Reddit, the author built *claude‑flow* itself using the same system — effectively a self-improving, modular engineering swarm ([reddit.com][2]).
- **Cost-effective scaling**: One developer comments you can run “a full AI R\&D team...for what you'd pay a junior dev for a few hours” ([reddit.com][2]).
- **Shared memory & monitoring**: With a CRDT-backed memory bank, agents coordinate knowledge and maintain coherence across tasks ([github.com][1]).

[1]: https://github.com/ruvnet/claude-code-flow?utm_source=chatgpt.com "ruvnet/claude-code-flow: This mode serves as a code-first orchestration ..."
[2]: https://www.reddit.com/r/ClaudeAI/comments/1l87dj7/claudeflow_multiagent_orchestration_platform_for/?utm_source=chatgpt.com "Multi-Agent Orchestration Platform for Claude-Code (npx claude-flow)"
[3]: https://codenotary.com/blog/using-claude-code-and-aider-to-refactor-large-projects-enhancing-maintainability-and-scalability?utm_source=chatgpt.com "Using Claude Code and Aider to Refactor Large Projects - Codenotary"

---

### 🎤 How to Use This Story in Your Talk

**Live narrative path:**

1. **Introduce**: “This isn't just hypothetical—look at *claude‑code‑flow*, where hundreds of agents collaborate on real code.”
2. **Explain the setup**: Describe the roles, shared memory, recursive development loop, and parallelism.
3. **Pull out lessons**:
   * Task orchestration > one-shot coding
   * Context sharing prevents duplication and inconsistencies
   * Monitoring + failure control = production readiness
4. **Contrast**: “Compare that to using a single Copilot window where context is lost per prompt.”
5. **Reinforce Do’s**: Highlight multi-stage prompts, memory, monitoring.
6. **Warn Don’ts**: Avoid unmanaged scaling, missing rollback logic, ignoring logs.

**Next steps?**

---

# Food for Thought

<!-- _class: table-with-mermaid -->
<!-- _no-fragment -->

<style scoped>
.table-with-mermaid {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 1.5rem;
  align-items: start;
}
.table-with-mermaid table {
  width: 100%;
  font-size: 0.9em;
  border-collapse: collapse;
}
.table-with-mermaid th,
.table-with-mermaid td {
  border: 1px solid #444;
  padding: 0.4em 0.6em;
}
</style>

Will future developers write code — or will they orchestrate teams of agents?

<div class="table-with-mermaid">

<!-- Column 1: Table -->
<div>

| Old World                     | AI-Driven World                   |
|------------------------------|-----------------------------------|
| Code as craft                | Code as raw material              |
| Syntax mastery               | System modeling mastery           |
| Framework expertise          | Problem decomposition expertise   |
| Boilerplate knowledge        | Context curation                  |
| Senior dev = language expert| Senior dev = systems orchestrator |

</div>

<!-- Column 2: Mermaid -->
<div>
  <div class="mermaid-container">
    <div class="mermaid">
      mindmap
        root((Future of AI Dev))
          Coding assistant
          Code review automation
          CI/CD integration
          Autonomous agents
          Regulatory challenges
          Prompt engineering skills
    </div>
  </div>
</div>

---

# What Actually Becomes Valuable

- 🧠 **Deep business understanding**
- 🔧 **Systems thinking and architecture**
- ⚙️ **Resilience engineering**
- 🧪 **Test design and coverage analysis**
- 🔍 **Code review & AI verification**
- 🎯 **Prompt engineering and instruction clarity**
- 🚦 **Ethical, regulatory, and safety oversight**
- Come back to do something fun in half an hour
---

# Takeaway

> "The AI writes more code.  
> The developer designs better systems."

---

# Q\&A

- Real-world experiences?
- Surprises with Copilot?
- Fears? Optimism?

---

# Thank You

**Markus / markus.hens@dk.ey.com**

*No Word. No PowerPoint. Only Markdown, Mermaid, and Code.*

---

