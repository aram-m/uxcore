# UX Core — Bob

A Claude plugin that surfaces relevant cognitive biases when you're building user-facing products. Powered by 105 biases and 63 curated product questions from [uxcore.io](https://keepsimple.io/uxcore) by Wolf Alexanyan / KeepSimple.

## What it does

Describe what you're building or the problem you're facing — and Bob tells you which psychological patterns apply, what to do about them, and what could backfire. With before/after visual demos.

Bob works two ways:
- **Building something?** (pricing page, onboarding, checkout, email) → Bob picks the most relevant biases and gives concrete actions
- **Diagnosing a problem?** ("why aren't our promotions working?", "users blame us for their mistakes") → Bob matches your problem to 63 curated product questions with pre-mapped bias recommendations

## Install

**Skills.sh (recommended):**
```bash
npx skills add aram-m/uxcore
```

**Claude Code (CLI):**
```bash
claude plugin marketplace add github:aram-m/uxcore
claude plugin install uxcore
```

**Claude.ai:**
Zip the `skills/bob/` directory and upload via Settings > Skills > Upload Skill.

## Usage

Invoke directly:
```
/bob I'm designing a cancellation flow for our SaaS
```

Or just describe a product/UX task — Bob auto-triggers on pricing, onboarding, checkout, copy, notifications, forms, A/B tests, and other user-facing work.

## Repo Structure

```
uxcore/
  .claude-plugin/
    plugin.json              <- Plugin manifest
  skills/
    bob/
      SKILL.md               <- Bob's personality, workflow, and instructions
      references/
        question-index.md    <- Index of 63 curated product questions with keywords
        questions.md         <- Full question entries with pre-mapped biases and answers
        bias-index.md        <- Quick-reference index of all 105 biases
        biases.md            <- Full bias descriptions with product/UX applications
        demo-recipes.md      <- 89 before/after visual scenarios
  SPEC.md                    <- Design spec (historical)
```

## Examples

**Building something:**
> "I'm designing a pricing page with three tiers: $9, $29, $99/mo"

Bob responds with relevant biases (Anchoring, Decoy Effect, Contrast Effect...), each with a concrete action for your specific tiers, an ASCII or HTML before/after demo, and a "Watch out" section flagging risks.

**Diagnosing a problem:**
> "Why aren't our promotions working? We've been running discounts but conversion is flat."

Bob matches this to a curated question, pulls pre-mapped biases (Curse of Knowledge, Conjunction Fallacy, Self-Reference Effect...) with contextual explanations of *why* each one applies to your situation, and adapts recommendations to your specific context.

## Credits

Biases and question dataset sourced from [UX Core](https://keepsimple.io/uxcore) by Wolf Alexanyan / KeepSimple.

## License

MIT
