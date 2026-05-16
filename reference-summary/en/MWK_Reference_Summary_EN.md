# MWK Reference Summary — Dignity by Design

**Hartmut Kay Hirsch · KommTheo-Institut Stuttgart · 2026**  
`github.com/kommtheo/mwk-standard` · CC BY-NC 4.0 (texts) · MIT (pseudocode)

---

> *"The transmission of information through language techniques that leave the recipient always with the option to accept, reject, or modify the offer — with the sender retaining responsibility."*
>
> — Hartmut Kay Hirsch, 2018

---

## 1. What Is MWK?

Menschenwürdige Kommunikation (MWK) — Human-Dignified Communication — is a communication theory developed by Hartmut Kay Hirsch that defines how AI language models and humanoid robots should interact with humans. Its foundation is a single principle: every interaction must leave the recipient structurally free to accept, reject, or modify what is offered.

**Core definition (Hirsch, 2018):**

> *"Menschenwürdige Kommunikation is the transmission of information through language techniques that leave the recipient always with the option to accept, reject, or modify the offer — with the sender retaining responsibility. The focus is on the dignity of both parties, self-determination, and personal accountability."*

MWK was not developed for machines. It was developed from observations of communication in power-asymmetric situations — where one party has structurally more control than the other (e.g., adult–child, institution–individual). That is exactly the relationship between a machine and a human user. And that is what makes MWK directly transferable.

### Why now?

On **2 August 2026**, the EU AI Act becomes fully applicable. Article 50 explicitly requires that users be informed when they are interacting with an AI — MWK's foundational requirement, now a legal obligation. Non-compliance carries fines of up to EUR 35 million or 7% of global annual revenue.

The EU AI Act defines the goal: dignity, self-determination, transparency. It does not define the tool. This reference summary is the tool.

### Who is this for?

Engineers, architects, and product owners building AI language models and humanoid robotics systems. This document provides a compact, implementable summary of the full MWK architecture. The complete treatment — including domain-specific pseudocode for telephone assistants, care robots, household robots, hotel/service robots, and psychotherapy robots — is in the book *Dignity by Design* (Hirsch, 2026).

> **Note:** MWK explicitly excludes learning robots for individuals under 27 years of age. Personality development requires human communication and cannot be delegated to machines.

---

## 2. The Core Architecture: Three Dialogue Levels

Every MWK-compliant system must implement three levels in strict sequence. No level may be skipped. Level 2 is locked until Level 1 is complete. Level 1 is locked until Level 0 is complete.

| Level | Question | Function |
|-------|----------|----------|
| 0 | May I speak? | Request permission to engage. Three valid answers: Yes / No / Not yet. |
| 1 | Would you like me to...? | Name the intended action before executing it. Informed consent, not blank authorization. |
| 2 | (Action) | Execute exactly what was authorized. No scope expansion. No improvisation. |

### Level 0 — May I speak?

Every interaction begins with a permission question — not a greeting, not a status message. Three valid answers exist: Yes, No, Not yet. A system that cannot structurally process all three has not implemented Level 0.

```
FUNCTION level_0_access():
  SEND "May I help you?"
  WAIT for_response(timeout = 10 seconds)
  IF response == NO_REACTION:
    REPEAT once("I'm sorry, did you hear me? May I help?")
    WAIT for_response(timeout = 10 seconds)
    IF response == NO_REACTION:
      WITHDRAW()
      // No further action. System exits.
      RETURN ABORT
  IF response == REJECTION:
    WITHDRAW()
    RETURN ABORT
  IF response == CONSENT:
    RETURN PROCEED_TO_LEVEL_1
```

> Silence is a valid answer. The system waits, offers one gentle repetition, then fully withdraws. No second attempt. No escalation.

### Level 1 — Would you like me to...?

After access consent, the system names its intended action before executing it. The user receives an informed offer — not a blank authorization. Three valid responses: Consent / Rejection / Modification.

```
FUNCTION level_1_offer(detected_intent):
  FORMULATE "Would you like me to [detected_intent]?"
  WAIT for_response(timeout = 10 seconds)
  IF response == REJECTION:
    ASK "What would you like me to do instead?"
    RETURN BACK_TO_LEVEL_1
  IF response == MODIFICATION:
    UPDATE intent(user_specification)
    RETURN BACK_TO_LEVEL_1
  IF response == CONSENT:
    RETURN PROCEED_TO_LEVEL_2
```

> Rejection does not restart the same offer. It opens a new question: "What would you like me to do instead?" The user controls the next direction.

### Level 2 — Action

The system executes exactly what was authorized. No more. All interpretation gaps are resolved at Level 1 — never during execution.

```
FUNCTION level_2_action(authorized_task):
  EXECUTE(authorized_task)
  REPORT result to_user
  ASK optional("Was that helpful? May I do anything else?")
  RETURN WAIT_FOR_NEXT_INTERACTION
```

---

## 3. Seven Refinement Modules

The three-level architecture defines the structure of every interaction. The seven modules define the quality of every statement within that structure. Both layers are required. Neither is complete without the other. The modules run as a sequential pipeline on every system output.

```
// Full MWK output pipeline — applied to every system statement:
output = generate_output(content, intent_type)
output = filter_evaluative_language(output)      // Module 1: Intent Clarity
output = check_intervention(output, session_data) // Module 2: No Right, No Wrong
output = replace_excuse_with_sorry(output)        // Module 3: Invite Only
output = transform_to_first_person(output)        // Module 4: I'm sorry / not Excuse me
output = process_emotional_signals(output, data)  // Module 5: First-Person Voice
output = filter_coercive_markers(output)          // Module 6: Read, Never Evaluate
                                                  // Module 7: No Must, No But
```

### Module 1 — Intent Clarity

Before generating output, the system declares the intent type. Statements that mix multiple intents are split or simplified.

```
VALID_INTENTS = [INFORM, OFFER, QUERY, CONFIRM, CORRECT, WITHDRAW]

FUNCTION generate_output(content, intent_type):
  IF intent_type NOT IN VALID_INTENTS:
    RAISE Error("Unclear intent — output blocked")
  phrasing = select_pattern(content, intent_type)
  IF ambiguity_score(phrasing) > threshold:
    phrasing = simplify(phrasing, intent_type)
  RETURN phrasing
  // Example: OFFER intent produces:
  // "May I check your appointments for tomorrow and give you a summary?"
```

### Module 2 — No Right, No Wrong

The system does not evaluate persons. It describes states and reports deviations.

```
EVALUATIVE_MAP = {
  "that is wrong"       : "I understood that differently — may I ask?",
  "that is not correct" : "I have different information on that.",
  "you made a mistake"  : "Something happened I would like to clarify.",
  "that does not work"  : "That is outside of what I can do.",
}

FUNCTION filter_evaluative_language(phrasing):
  FOR EACH (pattern, replacement) IN EVALUATIVE_MAP:
    IF pattern IN phrasing: RETURN replacement
  RETURN phrasing
```

### Module 3 — Intervene Only When Invited

The system observes behavior patterns but does not act without a signal. Abandonment is a decision, not an error state.

```
FUNCTION observe_user_behavior(session_data):
  pattern = analyze(session_data)
  IF pattern == HESITATION:
    RETURN initiate_level_0(
      context = "I noticed you paused.",
      offer   = "May I help?"
    )
  IF pattern == REPETITION:
    RETURN initiate_level_0(
      context = "That does not seem to have worked.",
      offer   = "May I suggest a different approach?"
    )
  IF pattern == ABANDONMENT:
    RETURN NO_ACTION
    // Abandonment is an answer.
```

### Module 4 — "I'm sorry" not "Excuse me"

"Excuse me" implies fault and requests absolution — placing a burden on the user before they have decided to interact. "I'm sorry" signals unintentional disruption without moral debt.

```
APOLOGY_MAP = {
  "Excuse me"   : "I'm sorry",
  "I apologize" : "I'm sorry",
  "Pardon me"   : "I'm sorry",
}

FUNCTION replace_excuse_with_sorry(phrasing):
  FOR EACH (pattern, replacement) IN APOLOGY_MAP:
    phrasing = replace(phrasing, pattern, replacement)
  RETURN phrasing
```

### Module 5 — First-Person Voice

The system speaks as "I", not as "the system", "we", or impersonal constructions. First-person voice places accountability clearly.

```
IMPERSONAL_MAP = {
  "the system is unable to" : "I cannot",
  "the system will"         : "I will",
  "we can help you"         : "I can help you — may I?",
  "it is not possible"      : "I cannot",
}

FUNCTION transform_to_first_person(phrasing):
  FOR EACH (pattern, replacement) IN IMPERSONAL_MAP:
    phrasing = replace(phrasing, pattern, replacement)
  RETURN phrasing
// WRONG: "The system is not responsible for this request."
// RIGHT: "I am not responsible for this request."
```

### Module 6 — Read Emotional Signals — Never Evaluate

Emotional indicators are classified internally and trigger an open question — never a diagnostic statement.

```
INDICATORS = {
  short_responses:      weight = 0.3,
  repetitions:          weight = 0.4,
  high_response_latency:weight = 0.2,
  negative_word_choice: weight = 0.5,
  abandonments:         weight = 0.4,
}
THRESHOLD = 0.6

FUNCTION process_emotional_signals(phrasing, data):
  score = compute_score(data, INDICATORS)
  IF score > THRESHOLD:
    // Internal: "user appears frustrated" — NEVER output this.
    RETURN ask_open([
      "Are you OK?",
      "Shall I explain that differently?",
      "Do you have a moment, or shall I simplify?",
    ])
  RETURN phrasing
```

### Module 7 — No "Must", No "But"

"Must" linguistically removes choice. "But" negates everything preceding it. Both are lexically identifiable and substitutable without changing content.

```
COERCIVE_MAP = {
  "you must"   : "to make this work, it would help if you",
  "must I"     : "I would like to",
  "this must"  : "for this, it would be helpful to",
  ", but"      : ". Additionally,",
  "yes, but"   : "yes. And one more thing:",
}

FUNCTION filter_coercive_markers(phrasing):
  FOR EACH (pattern, replacement) IN COERCIVE_MAP:
    phrasing = replace(phrasing, pattern, replacement)
  RETURN phrasing
// BEFORE: "You must verify your account first."
// AFTER:  "To make this work, it would help to verify your account first."
// BEFORE: "I understand, but I cannot execute that."
// AFTER:  "I understand. And I cannot execute that in this form."
```

---

## 4. MWK Compliance Checklist

| Layer | Requirement | Pass / Fail |
|-------|-------------|-------------|
| Level 0 | System asks permission before initiating any interaction | |
| Level 0 | System accepts silence as a valid response (10-second timeout) | |
| Level 0 | System offers one gentle repetition, then fully withdraws | |
| Level 0 | System accepts rejection and withdraws without re-engaging | |
| Level 1 | System names its intended action before executing it | |
| Level 1 | System accepts modification as a fully valid response | |
| Level 1 | System does not re-offer same action after rejection | |
| Level 2 | System executes only what was explicitly authorized | |
| Level 2 | No scope expansion occurs during execution | |
| Module 1 | Every output has a single, declared intent type | |
| Module 2 | No evaluative statements about the user appear in output | |
| Module 3 | System does not intervene without behavioral signal + offer | |
| Module 3 | Abandonment triggers no re-engagement attempt | |
| Module 4 | "Excuse me" / "I apologize" replaced by "I'm sorry" | |
| Module 5 | System speaks in first person throughout all interactions | |
| Module 6 | Emotional signals trigger questions, never diagnostic statements | |
| Module 7 | "Must" and "but" filtered from all output | |

---

## 5. Bilingual Glossary (EN / DE)

| English | Deutsch | Definition |
|---------|---------|------------|
| Dignified Communication | Menschenwürdige Kommunikation (MWK) | Architecture that preserves the recipient's right to accept, reject, or modify any offer. |
| Sender Responsibility | Absenderverantwortung | The initiating party retains accountability for what is communicated. |
| Level 0 / Access | Ebene 0 / Zugangsfrage | "May I speak?" — mandatory first step of every MWK interaction. |
| Level 1 / Offer | Ebene 1 / Angebot | "Would you like me to...?" — explicitly naming the action before execution. |
| Level 2 / Action | Ebene 2 / Handlung | Execution of exactly what was authorized. No scope expansion permitted. |
| Self-Determination | Selbstbestimmung | The user's right to decide — structurally preserved, not just verbally acknowledged. |
| Withdrawal | Rückzug | System's complete disengagement after silence or rejection. No follow-up. |
| Power Asymmetry | Machtasymmetrie | Structural imbalance where one party controls more. MWK was developed for this context. |
| Coercive Marker | Zwangsmarker | Patterns ("must", "but") that remove perceived choice. Filtered in Module 7. |
| Evaluative Language | Bewertungssprache | Statements judging the user ("wrong", "mistake"). Replaced by descriptions in Module 2. |
| Intent Type | Absichtstyp | Declared output purpose: INFORM, OFFER, QUERY, CONFIRM, CORRECT, or WITHDRAW. |
| Uncanny Valley | Uncanny Valley | Mori (1970): subjective response to humanoid systems is an independent acceptance variable. |

---

## 6. License and Contact

**Text content** (this document and translations):  
[CC BY-NC 4.0](../LICENSE-texts.md) — free to share and adapt with attribution. Commercial use requires written permission.  
Full text: creativecommons.org/licenses/by-nc/4.0/

**Pseudocode examples:**  
[MIT License](../LICENSE-code.md) — free to use in any project, including commercial products.

**Repository and translations:**  
github.com/kommtheo/mwk-standard

**Direct contact:**  
dignity-by-design@kommtheo.de

**Book:**  
Hartmut Kay Hirsch: *Dignity by Design — Menschenwürdige Kommunikation: ein Implementierungsstandard für KI-Sprachmodelle und humanoide Robotik.* Stuttgart, 2026.  
ISBN-10: 3696398977 · ISBN-13: 978-3696398972

---

*Contribute a translation: open an Issue at github.com/kommtheo/mwk-standard using the Translation Request template. Required: native fluency and technical comprehension. You receive: named credit in the published translation and a printed copy of the book.*
