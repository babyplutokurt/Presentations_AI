# MaxText Model Evaluation Tool — Deck System Design

## Deck Purpose & Narrative
- **Audience:** MaxText maintainers, AI platform leads, and reviewers listed in the design doc (Ran Ran, Gagik Amirkhanyan, Jacob Platin, Rich James, Jet Jiang).
- **Goal:** Sell the impact of Kurt Yang’s Google internship by walking through problem framing → design choices → solution architecture → measurable wins.
- **Tone:** Confident, product-quality storytelling with concise, data-backed messaging that mirrors the design doc while remaining presentation-friendly.

## Visual Language
- **Background:** `soft-mesh` module recolored to Google blue/red/yellow/green for brand alignment.
- **Layout System:** Large glassmorphism cards (`rounded-[32px]`, generous padding) for readability in fullscreen mode. Tabbed panels (`tab-pill`, `content-card`) follow the `ai-skill-tree` pattern to keep sections stable when switching content.
- **Typography & Emphasis:** Headline scale 5xl–7xl on hero, 3xl on internal slides; body copy sits at base–xl for legibility. Accent badges and gradient borders reuse the Google palette for hierarchy.
- **Reusable Components:**
  - Hero badge row for quick tagging of role, team, impact.
  - Tabbed “limitation vs requirement” and future “build vs adopt” panels for side-by-side narrative.
  - Requirement lists with color-coded bullets (sky for functional, emerald for performance).

## Slide Roadmap (current & planned)
| # | Slide Title | Purpose | Key Content & Visual Notes |
|---|-------------|---------|-----------------------------|
| 1 | **Kurt Yang’s Google Internship** | Establish who/what/where. | Built hero slide: title, subtitle (SWE Intern · AI Systems · Mountain View), badges for Engineering/AI/Impact, mentor quote card. |
| 2 | **Project 01 · MaxText Model Evaluation Tool** | TL;DR of flagship project plus requirements snapshot. | Built: TL;DR card, objective gradient card, functional vs non-functional requirement stacks. |
| 3 | **Problem Space & Requirements** | Surface current MaxText limitations and derived requirements. | Built: Tabbed panel (“Current Limitations” vs “Requirements”) mirroring `ai-skill-tree` tab style; title resized, body text enlarged for readability. |
| 4 | **Design & Framework Comparison** | Justify adopting standardized frameworks by contrasting them with bespoke scripts and comparing the top options. | **Built:** Uses a tabbed layout. **Tab 1 ("Individual Scripts"):** Frames as fast but unscalable. **Tab 2 ("Frameworks"):** Compares HuggingFace, Vertex AI, LM-Eval, and Evalchemy. **Tab 3 ("Decision"):** States the final choice to adopt LM-Eval + Evalchemy. |
| 5 | **Architecture: Server vs. Native** | Justify the choice of a decoupled server API over direct native integration into `lm-eval-harness`. | **Plan:** Use a side-by-side comparison. **Left Side (Native Integration):** Acknowledge this is a common pattern (vLLM, llama.cpp). List cons: **External Dependency** (slow PR reviews) and **Environment Conflicts** (maintenance burden). **Right Side (OpenAI Server API):** Frame as the preferred solution. List pros: **Full Decoupling** (independent upgrades) and **Standardized Interface**. |
| 6 | **The OpenAI-Compatible API** | Detail the user-facing API endpoints, showing how a client like `lm-eval-harness` would interact with them. | **Plan:** Use a tabbed interface to show code examples. **Tab 1 (`/v1/completions`):** Show a sample `curl` request and the corresponding JSON response for the legacy completions API. **Tab 2 (`/v1/chat/completions`):** Show a sample `curl` request and JSON response for the chat completions API. Emphasize that this is the standard interface `lm-eval` will use. |
| 7 | **Architecture Overview** | Illustrate the internal design of the server and how it connects evaluation frameworks to MaxText. | **Plan:** A single, clear architecture diagram. It will show: **`lm-eval-harness` (Client)** → **FastAPI Server (API Layer)** → **Internal Queue** → **MaxText Generator (Batch Inference on TPUs)**. This slide explains the implementation that powers the API from the previous slide. |
| 8 | **Core API Surface** | Detail the core backend APIs that enable the integration with evaluation frameworks. | **Plan:** Use a multi-column layout to detail the three core APIs: `generate_until` (for free-form generation), `loglikelihood` (for multiple-choice), and `loglikelihood_rolling` (for perplexity). Use code-style formatting for parameters and return types. |
| 9 | **Integration Plan** | Communicate the phased rollout strategy, showing a clear path from implementation to impact. | **Plan:** Use a horizontal timeline visual. **Phase 1 (OpenAI Server):** Note pros like decoupling and immediate broad coverage. **Phase 2 (Native LM-Eval Class):** Frame as a future enhancement for tighter integration, noting the external dependency. Mention "Individual Scripts" was rejected for scalability. |
| 10 | **Impact & Performance Wins** | Showcase the measurable improvements and project outcomes. | **Plan:** Use large metric tiles to display a "Before vs. After" comparison. **Coverage:** 1 → 189+ benchmarks. **Speed:** 30× faster evaluation (via batching). **Scalability:** Multi-node ready. |
| 11 | **Call to Action & Next Steps** | Close the presentation with clear, actionable next steps for the reviewers. | **Plan:** Use a clean list layout. **The Ask:** "Seeking approval for the proposed design." **Next Steps:** List key actions like merging the primary PR, publishing the updated README, and beginning Phase 2 planning. |

## Slide Production Guidance
- **Consistency:** Keep the broadened card sizes introduced on slides 1–3; use tabbed shells when showing alternate perspectives on the same problem.
- **Localization:** Deck remains English-only (`locale: 'en'`). Future translations can reuse the `locales/en.json` structure per slide key.
- **Assets:** Lightweight outline icons for architecture and metrics; avoid heavy imagery to maintain focus on narrative.
- **Interaction Hooks:** `ppt-container` thumbnails + progress help presenters jump to problem framing or impact during Q&A.

## Content Source Mapping
- **Slides 1–3:** Built from internship overview, TL;DR, and design-doc background/requirements.
- **Slide 4:** “Design” section evaluating custom scripts vs framework adoption.
- **Slide 5:** Framework comparison table in design doc.
- **Slide 6–7:** FR1/FR2/FR3, API descriptions, architecture notes.
- **Slide 8:** Solutions + Recommended Implementation Plan.
- **Slide 9:** Status updates, performance appendix, expectation section.
- **Slide10:** Approval table, project plan milestones, outstanding tasks.

Use this plan as the canonical reference while implementing the remaining slides so the narrative flows from problems → design decisions → architecture → execution → results without layout surprises.
