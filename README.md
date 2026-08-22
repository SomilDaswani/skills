# SKILLS

**A curated arsenal of Claude Code skills for writing, design, conversion, and prompt engineering.**

These are modular instruction packs that teach Claude how to perform specialized work with consistency and taste. Drop a folder into `~/.claude/skills/`, describe the task in chat (or invoke `/skill-name`), and Claude loads the playbook automatically.

Several skills in this collection read from `.claude/product-marketing-context.md` when it exists — a shared brand-voice file you can drop into any project so copywriting, editing, and CRO skills stay on-brand without repeating yourself.

This collection mixes **cloned community skills**, **forked frameworks**, and **original workflows** — all organized for one repo you can install, share, and extend.

---

## What's in the box

| Skill | Category | One-liner |
|-------|----------|-----------|
| [prompt-architect](./prompt-architect/) | Prompt Engineering | Score, diagnose, and rebuild prompts using 31 frameworks across 7 intent categories |
| [stop-slop](./stop-slop/) | Writing Quality | Strip AI writing tells from prose — filler phrases, formulaic structures, passive voice |
| [copywriting](./copywriting/) | Marketing Copy | Write conversion-focused copy for homepages, landing pages, pricing, and product pages |
| [copy-editing](./copy-editing/) | Marketing Copy | Seven-pass editing framework for polishing existing marketing copy without losing voice |
| [page-cro](./page-cro/) | Conversion | Analyze and optimize marketing pages — value prop, CTAs, trust signals, objection handling |
| [landing-page-auditor](./landing-page-auditor/) | Conversion | Structured audit of coach/consultant landing pages with outreach-ready top-3 issues |
| [frontend-design](./frontend-design/) | Design | Build distinctive, non-template UI with intentional typography, palette, and layout |
| [emil-design-eng](./emil-design-eng/) | Design Engineering | UI polish, animation decisions, and invisible details from Emil Kowalski's philosophy |
| [find-skills](./find-skills/) | Meta | Discover and install Claude skills from the open ecosystem via [skills.sh](https://skills.sh/) |
| [Upwork-proposal-writing](./Upwork-proposal-writing/) | Freelancing | Human-sounding Upwork proposals — frameworks, examples, and anti-AI-detection guide |

---

## How Claude Skills work

Each skill is a **directory with a `SKILL.md` file** at its root. Claude reads the YAML frontmatter (`name`, `description`) to decide when to invoke the skill, then follows the markdown instructions inside. Reference docs and assets load on demand — keeping your context window lean.

```
skill-name/
├── SKILL.md              # Required — main instructions + frontmatter
├── references/           # Optional — deep-dive docs loaded on demand
├── assets/               # Optional — templates, examples, scripts
└── scripts/              # Optional — executable helpers
```

**Where skills live in Claude Code:**

| Scope | Path | Applies to |
|-------|------|------------|
| **Personal** | `~/.claude/skills/<skill-name>/SKILL.md` | Every project on your machine |
| **Project** | `.claude/skills/<skill-name>/SKILL.md` | One repo — shareable via git |

On Windows, personal skills go in `%USERPROFILE%\.claude\skills\`.

Claude discovers skills at session start. If you add skills mid-session, restart Claude Code. Invoke directly with `/skill-name` or let Claude match from your message.

**Also works with:** Cursor (`~/.cursor/skills/`), and the Skills CLI (`npx skills add`) from [skills.sh](https://skills.sh/) — same format, different install path.

---

## Quick start

### Option A — Personal install (recommended)

Available in every Claude Code project on your machine.

**macOS / Linux:**

```bash
git clone https://github.com/SomilDaswani/skills.git
mkdir -p ~/.claude/skills

# Install individual skills
cp -r skills/prompt-architect ~/.claude/skills/
cp -r skills/stop-slop ~/.claude/skills/
cp -r skills/copywriting ~/.claude/skills/
# ... repeat for each skill you want
```

**Windows (PowerShell):**

```powershell
git clone https://github.com/SomilDaswani/skills.git
New-Item -ItemType Directory -Force -Path "$env:USERPROFILE\.claude\skills"

Copy-Item -Recurse skills\prompt-architect "$env:USERPROFILE\.claude\skills\"
Copy-Item -Recurse skills\stop-slop "$env:USERPROFILE\.claude\skills\"
# ... repeat for each skill you want
```

Verify a skill installed correctly:

```bash
ls ~/.claude/skills/prompt-architect/SKILL.md
```

The file must sit **directly** inside the skill folder — not nested one level deeper.

### Option B — Project install (team sharing)

Commit skills into a repo so teammates get the same playbooks:

```bash
mkdir -p .claude/skills
cp -r /path/to/skills/copywriting .claude/skills/
cp -r /path/to/skills/page-cro .claude/skills/
git add .claude/skills/
git commit -m "Add marketing CRO skills for Claude"
```

### Option C — Skills CLI

Install from GitHub once this repo is published:

```bash
npx skills add SomilDaswani/skills@prompt-architect -g -y
npx skills add SomilDaswani/skills@stop-slop -g -y
```

Browse the wider Claude skills ecosystem:

```bash
npx skills find copywriting
npx skills check
npx skills update
```

### Optional — Brand context file

For marketing skills (`copywriting`, `copy-editing`, `page-cro`), add a project-level context file:

```
your-project/
└── .claude/
    └── product-marketing-context.md   # Brand voice, audience, positioning
```

Claude reads this automatically before asking redundant questions.

### Using a skill in Claude

**Invoke directly:**

```
/prompt-architect
/stop-slop
/page-cro
```

**Or describe the task naturally** — Claude matches from the skill description:

| You say… | Skill that loads |
|----------|------------------|
| "Improve this prompt" | `prompt-architect` |
| "This sounds too AI-written" | `stop-slop` |
| "Write homepage copy for my SaaS" | `copywriting` |
| "Edit this landing page copy" | `copy-editing` |
| "Why isn't this page converting?" | `page-cro` |
| "Audit this landing page URL" | `landing-page-auditor` |
| "Build a distinctive hero section" | `frontend-design` |
| "Review my button animations" | `emil-design-eng` |
| "Find a skill for React testing" | `find-skills` |

---

## Repository structure

```
SKILLS/
│
├── README.md                          # You are here
│
├── prompt-architect/                  # ★ Largest skill — 31 prompt frameworks
│   ├── SKILL.md
│   ├── references/
│   │   ├── frameworks/                # 29 framework docs (CoT, RACE, CRISPE, …)
│   │   └── techniques/                # Composable techniques (few-shot, etc.)
│   └── assets/
│       └── templates/                 # Fill-in templates per framework
│
├── stop-slop/                         # Anti-AI-slop writing editor
│   ├── SKILL.md
│   └── references/
│       ├── phrases.md                 # Banned filler phrases
│       ├── structures.md              # Formulaic patterns to break
│       └── examples.md                # Before/after transformations
│
├── copywriting/                       # Conversion copywriter
│   ├── SKILL.md
│   └── refrences/                     # ⚠ See "Pre-push checklist" below
│       ├── copy-frameworks.md
│       └── natural-transitions.md
│
├── copy-editing/                      # Seven-sweeps copy editor
│   ├── SKILL.md
│   └── refrences/
│       └── plain-english-alternatives.md
│
├── page-cro/                          # Page conversion rate optimization
│   ├── SKILL.md
│   └── refrences/
│       └── experiments.md
│
├── landing-page-auditor/              # Coach/consultant page auditor
│   └── SKILL.md
│
├── frontend-design/                   # Distinctive UI design guidance
│   └── SKILL.md
│
├── emil-design-eng/                   # Design engineering craft
│   └── SKILL.md
│
├── find-skills/                       # Skills ecosystem discovery
│   └── SKILL.md
│
└── Upwork-proposal-writing/           # Freelance proposal playbooks
    ├── Anti-AI-Detection-Guide.md
    └── proposal-framework-examples.md
```

---

## Skill deep dives

### prompt-architect

The heavyweight of this collection. Analyzes any prompt on five dimensions (Clarity, Specificity, Context, Completeness, Structure), scores it 1–10, routes to one of **31 frameworks** based on intent, and emits a polished result.

**Intent categories:** Recover · Clarify · Create · Transform · Reason · Critique · Agentic

**Includes:** 29 framework reference docs, few-shot technique guide, and 30+ copy-paste templates in `assets/templates/`.

**Upstream:** [ckelsoe/prompt-architect](https://github.com/ckelsoe/prompt-architect) (MIT)

---

### stop-slop

A prose linter for the AI era. Eight core rules — cut filler, break formulaic structures, active voice, specificity, reader-in-the-room voice, rhythm variation, trust the reader, kill pull-quotes. Ships with phrase blacklists, structural pattern guides, and scored before/after examples.

**Upstream:** [Hardik Pandya](https://hvpandya.com) (MIT)

---

### copywriting + copy-editing

A matched pair for marketing copy. **Copywriting** gathers context (page type, audience, offer, traffic source) and writes benefit-driven, specific copy with headline formulas and page templates. **Copy-editing** runs seven sequential sweeps — Clarity, Voice, So What, Prove It, Specificity, Heightened Emotion, Zero Risk — so each pass catches what a single review misses.

Both skills check for `.claude/product-marketing-context.md` in your project before asking questions — set up brand voice once, reuse everywhere.

Reference docs cover headline formulas, page structure templates, natural transitions, and plain-English word swaps.

---

### page-cro + landing-page-auditor

**page-cro** is the full CRO analyst — value proposition clarity, headline effectiveness, CTA hierarchy, visual scannability, trust signals, objection handling, and page-type-specific guidance (homepage, landing, pricing, blog).

**landing-page-auditor** is the lightweight specialist for coach/consultant pages. Give it a URL, get a categorized audit plus three cold-email-ready issues. Built for outreach workflows.

---

### frontend-design + emil-design-eng

**frontend-design** pushes agents away from the three default AI aesthetics (warm cream serif, dark acid-green, broadsheet newspaper) toward subject-driven, distinctive design. Covers token systems, type pairing, signature elements, motion restraint, and interface copy.

**emil-design-eng** encodes Emil Kowalski's design engineering philosophy — animation frequency rules, easing curves, `:active` states, transform-origin for popovers, and a required Before/After/Why review table format. Points to [animations.dev](https://animations.dev/) for deeper learning.

---

### find-skills

Meta-skill for the skills ecosystem. Teaches agents to search [skills.sh](https://skills.sh/), verify install counts and source reputation, and recommend `npx skills add` commands. Includes quality gates (prefer 1K+ installs, official sources, GitHub star checks).

---

### Upwork-proposal-writing

Original freelancing playbook — not yet a formal Agent Skill (see checklist below). Contains:

- **proposal-framework-examples.md** — The proven ~200-word structure: hook → understanding → qualifications → value prop → portfolio → CTA with questions
- **Anti-AI-Detection-Guide.md** — Structural red flags, 50 forbidden AI phrases, human writing patterns, and client-side detection tactics

---

## Skill relationships

Some skills reference siblings that aren't in this repo yet (they exist in upstream marketing-skills collections):

```
copywriting ──► copy-editing        (polish after drafting)
page-cro ──────► copywriting        (rewrite if copy is the bottleneck)
page-cro ──X──► signup-flow-cro     (not included — upstream only)
page-cro ──X──► form-cro            (not included — upstream only)
stop-slop ◄──── copy-editing        (complementary anti-AI passes)
frontend-design ◄── emil-design-eng (design vision ↔ craft polish)
```

If you install the full upstream marketing skills pack later, the cross-references in `page-cro` and `copywriting` will resolve automatically.

---

## Pre-push checklist

Review these structural items before publishing to GitHub:

### Fix before push (broken references)

| Issue | Location | Fix |
|-------|----------|-----|
| **`refrences/` typo** | `copywriting/`, `copy-editing/`, `page-cro/` | Rename folder to `references/` — SKILL.md links already point to `references/` |
| **Missing framework file** | `landing-page-auditor/SKILL.md` line 12 | Create `auditor-framework.md` or update the skill to inline the framework |
| **Missing license file** | `frontend-design/SKILL.md` frontmatter | Add `LICENSE.txt` or remove the license field from frontmatter |

### Recommended improvements

| Issue | Location | Suggestion |
|-------|----------|------------|
| **No SKILL.md** | `Upwork-proposal-writing/` | Add a `SKILL.md` with frontmatter that points to the two existing guides |
| **Naming inconsistency** | `Upwork-proposal-writing/` | Consider renaming to `upwork-proposal-writing` (kebab-case matches every other skill) |
| **No root LICENSE** | repo root | Add a LICENSE file — skills have mixed licenses (MIT, upstream terms) |
| **Encoding artifacts** | `Upwork-proposal-writing/*.md` | Some files have mojibake (`â€"`, `âŒ`) — re-save as UTF-8 |
| **No `.gitignore`** | repo root | Add one if you don't want OS junk (`.DS_Store`, `Thumbs.db`) |

### What's already solid

- Every core skill (except Upwork) has a valid `SKILL.md` with YAML frontmatter
- `prompt-architect` is the most complete — references, templates, and progressive loading instructions
- `stop-slop` follows the ideal pattern: lean SKILL.md + lazy-loaded reference docs
- Consistent kebab-case naming across 9 of 10 folders
- Skills are self-contained — no external dependencies required to run

---

## Credits & attribution

This collection stands on the shoulders of excellent open work. Please retain upstream licenses when modifying or redistributing individual skills.

| Skill | Author / Source | License |
|-------|-----------------|---------|
| prompt-architect | [ckelsoe](https://github.com/ckelsoe/prompt-architect) | MIT |
| stop-slop | [Hardik Pandya](https://hvpandya.com) | MIT |
| frontend-design | Anthropic skills collection | See upstream LICENSE.txt |
| find-skills | skills.sh ecosystem | — |
| copywriting, copy-editing, page-cro | Marketing skills ecosystem (upstream) | — |
| emil-design-eng | Based on [Emil Kowalski](https://emilkowal.ski/)'s design engineering philosophy | — |
| landing-page-auditor, Upwork-proposal-writing | Original to this collection | — |

If you are an upstream author and want attribution adjusted or your skill removed, open an issue.

---

## Adding your own skill

1. Create a folder with kebab-case naming: `my-new-skill/`
2. Add `SKILL.md` with frontmatter:

```markdown
---
name: my-new-skill
description: What it does and when to trigger it. Be specific — Claude uses this to decide. Include trigger phrases.
---

# My New Skill

## Instructions
Step-by-step guidance here.
```

3. Keep `SKILL.md` under ~500 lines; offload detail to `references/`
4. Install to `~/.claude/skills/my-new-skill/` and test with `/my-new-skill` or a natural-language prompt
5. Submit a PR or drop the folder in this repo

See the [Claude Code skills docs](https://code.claude.com/docs/en/skills) or run `npx skills init my-new-skill` for scaffolding.

---

## FAQ

**Do I need all of these?**  
No. Install only what you use. `prompt-architect` + `stop-slop` cover most writing tasks. Add CRO and design skills when you need them.

**Why isn't my skill showing up?**  
Check that `SKILL.md` sits directly in `~/.claude/skills/<name>/` (not nested deeper), restart Claude Code if you added it mid-session, and run `/doctor` if descriptions are being truncated.

**Will these work with Cursor or ChatGPT?**  
These are built for **Claude Code**. The same `SKILL.md` format also works in Cursor (`~/.cursor/skills/`). ChatGPT and Copilot don't auto-trigger skills, but you can paste the instructions manually.

**Can I fork one skill without the rest?**  
Yes. Each folder is independent. Respect the upstream license.

**Why a separate repo instead of `~/.claude/skills/`?**  
This repo is your portable library — version-controlled, shareable, and easy to clone into Claude's skills directory or commit into project repos.

---

## License

Individual skills carry their own licenses (see Credits above). This repository as a collection does not override upstream terms. Add a root `LICENSE` before publishing if you want explicit terms for original content in this repo.

---

<p align="center">
  <strong>Teach Claude to write like humans, design with taste, and optimize like analysts.</strong><br>
  Star the repo if a skill saved you from shipping slop.
</p>
