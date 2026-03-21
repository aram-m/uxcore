# UX Core — Bob

A Claude skill that surfaces relevant cognitive biases when you're building user-facing products. Powered by 105 biases from [uxcore.io](https://keepsimple.io/uxcore) by Wolf Alexanyan / KeepSimple.

## What it does

Describe what you're working on — a pricing page, onboarding flow, checkout, email campaign, landing page, notification, form — and Bob tells you which psychological patterns apply, what to do about them, and what could backfire. With before/after visual demos.

## Install

**Claude Code (CLI):**
```
Copy skills/bob/ to ~/.claude/skills/bob/
```

**Claude.ai:**
Upload `bob.skill` (or zip the `skills/bob/` directory) via Settings > Skills > Upload Skill.

## Usage

Invoke directly:
```
/bob I'm designing a cancellation flow for our SaaS
```

Or just describe a product/UX task — Bob auto-triggers on pricing, onboarding, checkout, copy, notifications, forms, A/B tests, and other user-facing work.

## What's inside

- `skills/bob/SKILL.md` — Bob's personality, workflow, and instructions
- `references/bias-index.md` — Quick-reference index of all 105 biases
- `references/biases.md` — Full bias descriptions with product/UX applications
- `references/demo-recipes.md` — 89 before/after visual scenarios

## Example

> "Our checkout page has a 68% cart abandonment rate. Users add items but bail at payment."

Bob responds with 3-5 relevant biases (Loss Aversion, Zero-Risk Bias, Ambiguity Effect, Reactance...), each with a concrete action, an ASCII or HTML before/after demo, and a "Watch out" section flagging risks.

## Credits

Biases sourced from [UX Core](https://keepsimple.io/uxcore) by Wolf Alexanyan / KeepSimple.
