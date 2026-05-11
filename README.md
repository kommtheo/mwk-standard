# MWK Standard — Dignified Communication for AI Systems

**Menschenwürdige Kommunikation (MWK)** is a communication theory developed by Hartmut Kay Hirsch that defines how AI language models and humanoid robots should interact with humans — based on three structural principles: permission, offer, and action only after explicit consent.

This repository supports the book **Dignity by Design** (Hirsch, 2026) and contains:

- 📄 **English Reference Summary** — a concise guide to the MWK architecture for international engineering teams
- 🌍 **Translations** — community-contributed translations of the Reference Summary
- 📋 **Pseudocode patterns** — implementation examples for five application domains

---

## What is MWK?

MWK defines dignified communication as:

> *The transmission of information through language techniques that leave the recipient always with the option to accept, reject, or modify the offer — with the sender retaining responsibility.*

The core architecture operates on three levels:

| Level | Question | Purpose |
|-------|----------|---------|
| 0 | May I speak? | Ask permission to engage |
| 1 | Would you like me to…? | Formulate the offer |
| 2 | (Action) | Execute only after explicit consent |

Silence is an answer. The system waits (~10 seconds), offers one gentle repetition, then withdraws.

---

## Repository Structure

```
mwk-standard/
├── README.md
├── CONTRIBUTING.md
├── LICENSE                    ← CC BY-NC 4.0 (texts)
├── LICENSE-CODE               ← MIT (pseudocode)
├── reference-summary/
│   └── en/                    ← English Reference Summary (PDF, coming at publication)
└── translations/
    ├── zh-CN/                 ← Mandarin Chinese (open for contribution)
    ├── ja/                    ← Japanese (open for contribution)
    ├── ko/                    ← Korean (open for contribution)
    ├── es/                    ← Spanish (open for contribution)
    ├── pt-BR/                 ← Brazilian Portuguese (open for contribution)
    ├── ar/                    ← Arabic (open for contribution)
    ├── hi/                    ← Hindi (open for contribution)
    └── fr/                    ← French (open for contribution)
```

---

## Five Application Domains (covered in the book)

1. **Telephone Assistant** — consent-based call handling and redirection
2. **Care Robot** — dignified interaction with vulnerable users
3. **Household Robot** — privacy-aware domestic communication
4. **Hotel & Service Robot** — hospitality interactions at scale
5. **Psychotherapy Robot** — high-sensitivity dialogue in therapeutic contexts

Each domain includes pseudocode for the MWK three-level architecture and all seven refinement modules.

---

## License

- **Texts** (Reference Summary, documentation): [Creative Commons BY-NC 4.0](LICENSE)
  Sharing is explicitly encouraged. Commercial use of the texts without written permission is not permitted.
- **Pseudocode examples**: [MIT License](LICENSE-CODE)
  Free to use, including in commercial products.

---

## Contributing a Translation

We are looking for **idealist translators** — engineers, communication researchers, and native speakers — who share the conviction that machines can and should be built to respect human self-determination.

What you bring: native fluency, technical understanding, and time.
What you get: your name in the published translation and a printed copy of the book.

→ See [CONTRIBUTING.md](CONTRIBUTING.md) to get started.

---

## Contact

- Issues and pull requests: use GitHub Issues (preferred)
- Direct contact: dignity-by-design@kommtheo.de

---

## About the Author

**Hartmut Kay Hirsch** is the founder of the MWK theory and the KommTheo-Institut in Stuttgart, Germany. He developed and field-tested MWK since 2018 in pedagogical power-asymmetry contexts. *Dignity by Design* (2026) is its first systematic application to AI language models and humanoid robotics.

Book: [www.kommtheo.de/kayhirsch/#dignity-by-design](https://www.kommtheo.de/kayhirsch/#dignity-by-design) Coming plan in June 2026

