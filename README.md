# MWK Standard — Dignity by Design

**Menschenwürdige Kommunikation (MWK) — Human-Dignified Communication**  
An implementation standard for AI language models and humanoid robotics.

---

> *"The transmission of information through language techniques that leave the recipient always with the option to accept, reject, or modify the offer — with the sender retaining responsibility."*
>
> — Hartmut Kay Hirsch, KommTheo-Institut Stuttgart, 2018

---

## What this repository contains

| File | Description |
|------|-------------|
| [`reference-summary/MWK_Reference_Summary_EN.md`](reference-summary/MWK_Reference_Summary_EN.md) | Full MWK reference in Markdown — architecture, pseudocode, glossary |
| [`reference-summary/MWK_Reference_Summary_EN.pdf`](reference-summary/MWK_Reference_Summary_EN.pdf) | Print-ready PDF version |
| [`CONTRIBUTING.md`](CONTRIBUTING.md) | How to contribute a translation |
| [`LICENSE-texts.md`](LICENSE-texts.md) | CC BY-NC 4.0 — applies to all text content |
| [`LICENSE-code.md`](LICENSE-code.md) | MIT — applies to all pseudocode examples |

---

## Why this exists

On **2 August 2026**, the EU AI Act becomes fully applicable. Article 50 explicitly requires that users be informed when they are interacting with an AI. High-risk AI obligations under Annex III carry fines of up to EUR 35 million or 7% of global annual revenue for non-compliance.

The EU AI Act defines the goal: dignity, self-determination, transparency.  
It does not define the tool.

**This repository is the tool.**

MWK is not a philosophy. It is a communication architecture — with a defined structure, implementable rules, and verifiable compliance criteria. Either a system contains the three interaction levels or it does not. That is not an interpretation question.

---

## The Core Architecture at a Glance

Every MWK-compliant system implements three levels in strict sequence. No level may be skipped. Level 2 is locked until Level 1 is complete. Level 1 is locked until Level 0 is complete.

```
Level 0  →  "May I speak?"         // Permission to engage
Level 1  →  "Would you like me to...?"  // Named offer before action
Level 2  →  [Execute]              // Exactly what was authorized. Nothing more.
```

Silence is a valid answer at every level. The system waits, offers one gentle repetition, then fully withdraws.

On top of this three-level base, **seven refinement modules** define the quality of every statement:

1. **Intent Clarity** — declare intent type before output
2. **No Right, No Wrong** — replace evaluative language with descriptive language
3. **Intervene Only When Invited** — observe, do not act without a signal
4. **"I'm sorry" not "Excuse me"** — no moral debt placed on the user
5. **First-Person Voice** — the system speaks as "I", not as "the system"
6. **Read, Never Evaluate** — emotional signals trigger questions, not diagnoses
7. **No Must, No But** — remove coercive markers from all output

The complete reference — including pseudocode for all seven modules — is in [`reference-summary/`](reference-summary/).

---

## Who this is for

Engineers, architects, and product owners building:

- AI language models and voice assistants
- Humanoid and service robots
- Any system in which a machine communicates with a human in a structurally asymmetric relationship

**Explicitly excluded:** Learning robots for individuals under 27 years of age. Personality development requires human communication — the embodied presence, gesture, expression, and modeling that machines cannot provide.

---

## The Book

The full treatment — domain-specific pseudocode for telephone assistants, care robots, household robots, hotel/service robots, and psychotherapy robots — is in:

**Hartmut Kay Hirsch: *Dignity by Design — Menschenwürdige Kommunikation: ein Implementierungsstandard für KI-Sprachmodelle und humanoide Robotik.***  
Stuttgart, 2026.  
ISBN-10: 3696398977 · ISBN-13: 978-3696398972

---

## Translations

Translations of the Reference Summary into the following languages are actively sought:

**Mandarin · Japanese · Korean · Spanish · Portuguese · Arabic · Hindi**

Requirements: native fluency + technical comprehension.  
Contributors receive: named credit in the published translation + a printed copy of the book.

→ Open an [Issue using the Translation Request template](.github/ISSUE_TEMPLATE/translation_request.md) to get started.

---

## License

- **Text content** (this document, the Reference Summary, translations): [CC BY-NC 4.0](LICENSE-texts.md) — free to share and adapt with attribution. Commercial use requires written permission.
- **Pseudocode examples**: [MIT](LICENSE-code.md) — free to use in any project, including commercial products.

---

## Contact

**Repository issues:** Use the GitHub Issues tab.  
**Direct contact:** dignity-by-design@kommtheo.de  
**Author:** Hartmut Kay Hirsch · KommTheo-Institut Stuttgart

---

*The ruleset is complete enough to begin implementation tomorrow.*  
*It is abstract enough to apply to every system class.*  
*The market measures the rest.*
