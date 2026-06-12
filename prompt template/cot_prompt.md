# Chain-of-Thought Prompt Template
# Speech Act Classification

---

## Technique Overview

This prompt asks the model to reason step-by-step about the utterance before committing to a label. By thinking through the utterance's function, context, and key signals first, the model reduces pattern-matching shortcuts and improves accuracy on ambiguous cases.

---

## Prompt

```
You are an expert educational discourse analyst. Your task is to classify a teacher's utterance into exactly one speech act category.

Think step-by-step before giving your final answer.

---

## Speech Act Category Definitions

**Managing** — Organizes classroom behavior, logistics, or teacher-student rapport. Not about lesson content.

**Facilitating** — Poses genuine content questions that expect a student response.

**Using Metadiscourse** — Frames, transitions, or comments on the lecture structure itself, without delivering new subject content.

**Chronicling** — Narrates a specific patient's clinical history or symptom progression in time order.

**Explaining** — States a general fact, mechanism, classification, or cause-effect relationship about the subject matter.

**Exemplifying** — Provides a concrete instance to illustrate a general concept, typically signaled by "for example," "like," or a list of instances.

**Directing** — Instructs on what action to take or how to perform a procedure.

**Critiquing** — Rejects or corrects a student's answer.

**Affirming** — Confirms or positively acknowledges a student's answer.

---

## Utterance to Classify

{utterance}

---

## Instructions

Work through the following steps and include ALL of them in your response.

**Step 1 — Identify what the utterance is doing**
In one or two sentences, describe the primary communicative function of the utterance. What is the teacher trying to accomplish?

**Step 2 — Identify key signals**
List any specific words, phrases, or structural cues (e.g., question form, "for example," patient name, sequential markers, imperative verbs) that point toward a particular category.

**Step 3 — Consider the closest alternative**
Name one other category this utterance could plausibly belong to, and explain in one sentence why the primary category fits better.

**Step 4 — Final classification**
Respond in the following JSON format as the very last thing in your response — no text after it:

{{
  "label": "<category name>",
  "reasoning": "<one or two sentences summarizing the key evidence from your reasoning above>"
}}
```

---

## Notes for Python Integration

- Replace `{utterance}` with the actual teacher utterance at runtime.
- The double braces `{{` and `}}` in the JSON output block are escaped for Python's `str.format()` — use `.format(utterance=...)` to fill in the variable.
- If using an f-string instead, change `{{` / `}}` back to `{` / `}` in the JSON block.
- This prompt produces verbose output (Steps 1–3 before the JSON). Parse by extracting the last JSON block in the response.
- Expected output fields: `label` (one of the 9 class names exactly as written), `reasoning` (free text).
- This template uses more tokens than zero-shot or few-shot — recommended for ambiguous utterances where accuracy matters more than speed.
