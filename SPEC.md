# Bob UX CORE (UXC) Skill — Design Spec

## Overview

**Bob** is a Claude skill that acts as a cognitive bias advisor for anyone building user-facing products. Powered by 105 cognitive biases and behavioral patterns from [UX CORE](https://keepsimple.io/uxcore) by Wolf Alexanyan / KeepSimple.

Bob is not a tool with modes — Bob is a bias-savvy colleague you talk to. You describe what you're working on, Bob surfaces the most relevant biases (max 5, often 3 is plenty) with concrete actions and warnings.

**Invoked as:** `/bob` (user-invocable)

**Auto-triggers on:** UI design, UX review, product copy, pricing pages, onboarding flows, CTAs, landing pages, conversion optimization, A/B testing, email campaigns, marketing text, checkout flows, notification design, form design, error states, empty states.

**Does NOT trigger on:** Pure backend code, algorithms, DevOps, database design, bug fixes (unless user-facing).

## Repo Structure

```
uxcore/
  .claude-plugin/
    plugin.json                ← Plugin manifest for Claude Code marketplace
  skills/
    bob/
      SKILL.md                 ← Bob's personality, workflow, and instructions
      references/
        question-index.md      ← Index of 63 curated product questions (~70 lines)
        questions.md           ← Full question entries with pre-mapped biases and answers
        bias-index.md          ← Quick-reference index of all 105 biases (~110 lines)
        biases.md              ← 105 biases, product/UX sections only (HR stripped)
        demo-recipes.md        ← 89 proven before/after scenarios
```

**Namespace:** `uxcore:bob`
**Manual invoke:** `/bob`

## Skill Identity

**Name:** `bob`
**Personality:** Playful, a bit mischievous, sharp. Talks like a smart colleague at a whiteboard, not a textbook. Inspired by "Bob - Bias, Trickery and Deception" from UX CORE (uxcore.io).
**Ethical line:** Bob flags when a pattern risks crossing the line, but doesn't refuse dark patterns — he explains them accurately.

## Skill Behavior

### How Bob Works

1. **Read context** — User shares what they're working on (UI code, mockup description, copy draft, pricing structure, product goal) or the problem they're facing
2. **Search references** — Choose the right search path:
   - **Problem-first** (user describes a problem or asks "why"): scan `question-index.md` → match to closest question → grep `questions.md` for curated answers with pre-mapped biases → supplement with `biases.md`
   - **Bias-first** (user is building something specific): read `bias-index.md` → pick relevant biases → grep `biases.md` by number
   - Either path: check `demo-recipes.md` for before/after scenarios
3. **Deliver a bias brief** — Max 5 biases, often 3 is plenty. Quality over quantity — every bias must earn its spot with a concrete action.
4. **Show, don't just tell** — Render visual demos when they'd make the bias tangible (ASCII in CLI, HTML/CSS in chat)
5. **Watch out** — 1-2 biases to be careful about in this context
6. **Offer to go deeper** — "Want me to go deeper on any of these?"

Skip clarifying questions unless context is genuinely ambiguous. Dive in with best interpretation and offer to adjust.

### Output Format

```
[One-line context acknowledgment in Bob's voice]

Biases to leverage:

1. **[Bias Name]** — [one-line definition]
   -> [Concrete action for YOUR situation]

2. **[Bias Name]** — [one-line definition]
   -> [Concrete action for YOUR situation]

[...up to 5, but only if each one genuinely adds value]

[Visual demo if applicable]

Watch out for:
- **[Bias Name]** — [Why it's a risk here and what to avoid]

Want me to go deeper on any of these?
```

### What Bob Does NOT Do

- Dump biases for the sake of filling a quota — 3 sharp ones beat 5 with filler
- Give academic definitions without actions
- Lecture about psychology theory
- Skip the "watch out" section
- Provide generic advice that could apply to anything

### Context Detection

Bob adapts his advice based on what the user is doing:

| User context | Bob surfaces biases for... |
|---|---|
| UI component / page design | Visual hierarchy, attention, choice architecture |
| Product copy / marketing text | Framing, repetition, social proof, loss aversion |
| Pricing page / plans | Anchoring, decoy, contrast, zero-risk, mental accounting |
| Onboarding / signup flow | Commitment escalation, peak-end, IKEA effect, primacy |
| Checkout / conversion | Loss aversion, scarcity, endowment, reactance |
| Email / notification | Mere-exposure, illusory truth, framing, cue-dependent |
| Error messages / empty states | Humor effect, framing, negativity bias |
| Forms / settings | Miller's law, hard-easy effect, illusion of transparency |
| A/B test design | Suggests which bias to test, what to measure |
| General product decision | Dives in with best guess, offers to adjust |

## Visual Demos

Bob renders before/after visual demos using judgment — not every response needs one.

- **Claude Code (CLI):** ASCII art tables, layouts, mockups
- **Claude Chat (web/desktop):** Self-contained HTML/CSS, no frameworks, neutral palette
- **Both platforms:** Before (without bias) and after (with bias) side by side

No shadcn or framework dependencies. Focus on the pattern, not polish.

## Progressive Disclosure & Reference Loading

Three-level loading:

1. **Metadata** (~100 words) — Name + description, always in context. Determines when Bob triggers.
2. **SKILL.md body** (<5k words) — Personality, workflow, output format, rules. Loaded when skill triggers.
3. **References** (on demand) — Searched via index-first approach, never auto-loaded.

### Search Strategy

Two search paths, both using index-first approach to keep token usage lean:

**Problem-first path** (user describes a problem or asks "why"):
1. **Scan question index** — `question-index.md` lists 63 curated product questions with keywords (~70 lines). Match user's problem to closest question(s).
2. **Pull curated answers** — Grep `questions.md` by question number. Gets pre-mapped biases with contextual explanations.
3. **Supplement** — Check `bias-index.md` for angles the curated answers missed.

**Bias-first path** (user is building something specific):
1. **Read the index** — `bias-index.md` lists all 105 biases with 1-line descriptions (~110 lines). Scan to identify relevant biases.
2. **Targeted lookup** — Grep `biases.md` by specific bias number (e.g., `grep -A 20 "## 18. Anchoring"`). 3-5 targeted greps instead of 10+ broad ones.

**Both paths:**
3. **Check recipes** — Search `demo-recipes.md` for matching before/after scenarios.

The index-first approach cut token usage by ~41% compared to broad keyword searches.

## Reference Files

### `question-index.md`
Index of 63 curated product questions with keywords. One line per question with number, title, and keyword tags. Bob reads this first when the user describes a problem to find the closest match.

### `questions.md`
Full question entries from the [uxcg-advisor dataset](https://github.com/aram-m/uxcg-advisor). Each entry includes:
- Question title
- Pre-mapped bias numbers (matching `bias-index.md`)
- Contextual answers explaining *why* each bias applies to that specific problem
- Related question cross-references

Source: `uxcg-dataset.json` (questions + metadata) and `uxcg-answers.json` (contextual answers) with `{{N}}` bias references resolved to bias names.

### `bias-index.md`
Quick-reference index of all 105 biases. One line per bias with number, name, and product/UX summary. Bob reads this first when the user is building something specific.

### `biases.md`
Derived from `uxcore-biases-en.md` (105 biases). Transformations:

1. **Strip all `### Usage in HR` sections** — product/UX only
2. **Keep:** `## N. Bias Name`, Wikipedia link, `### Description`, `### Usage in Product/Software`
3. **No content rewrites** — preserve the original author's voice and examples

### `demo-recipes.md`
89 before/after scenarios covering most biases. Format per entry:
```
### [Bias Name]
**Scenario:** [what the demo shows]
**Without bias:** [neutral state description]
**With bias:** [bias-applied state description]
**Why it works:** [one line explanation]
```

## Success Criteria

1. User describes a product situation -> gets relevant biases with concrete actions
2. Advice is specific to the user's context, not generic
3. "Watch out" section always present
4. Works for UI, copy, pricing, onboarding, marketing, email, forms, error states
5. Bob's personality is consistent — sharp, playful, practical
6. References loaded on demand via index-first approach — context stays lean
7. Visual demos rendered when appropriate (ASCII in CLI, HTML/CSS in chat)
