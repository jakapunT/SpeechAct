# Contrastive Pair Generation Prompt Template
# Speech Act Classification

---

## Technique Overview

This prompt presents side-by-side contrastive pairs — utterances that are superficially similar but belong to different classes. Each pair is chosen to highlight the single distinguishing feature that separates the two categories. This is especially useful for the class boundaries that produce the most annotator disagreement in this dataset.

---

## Prompt

```
You are an expert educational discourse analyst. Your task is to classify a teacher's utterance into exactly one speech act category.

The following contrastive pairs show utterances that look alike but belong to different categories. Study them to understand the key distinctions before classifying the utterance at the end.

---

## Contrastive Pairs

### Pair 1 — Facilitating vs. Using Metadiscourse
The difference: Facilitating genuinely expects a student to answer. Using Metadiscourse uses question-like forms only to mark lecture flow or seek agreement — no real student response is expected.

| Label | Utterance |
|---|---|
| Facilitating | "So what is the motor cortex?" |
| Using Metadiscourse | "Right?" (said after stating a fact, seeking listener agreement) |
| Facilitating | "According to the CDC, what is the incubation period for this disease?" |
| Using Metadiscourse | "And for this week, we'll focus on the voluntary motor system." |

Key rule: If the teacher is actually waiting for a student to answer, it is Facilitating. If the question-like form is a discourse marker or rhetorical device, it is Using Metadiscourse.

---

### Pair 2 — Explaining vs. Using Metadiscourse
The difference: Explaining delivers factual content about the subject. Using Metadiscourse talks about the lecture itself — its structure, scope, or direction — without adding new subject content.

| Label | Utterance |
|---|---|
| Explaining | "The nervous system can be divided into the sensory and motor system." |
| Using Metadiscourse | "This week we will focus on three specific areas of the nervous system." |
| Explaining | "Smoking can lead to lung damage and increase the risk of cancer." |
| Using Metadiscourse | "And now, let's move to the next subtopic, which is the motor cortex." |

Key rule: Ask "Is the teacher saying something true about the world/body/disease, or about the lecture?" If about the lecture — Metadiscourse.

---

### Pair 3 — Explaining vs. Exemplifying
The difference: Explaining states a general fact or mechanism. Exemplifying provides a concrete instance to illustrate a concept, usually signaled by "for example," "like," or "such as."

| Label | Utterance |
|---|---|
| Explaining | "The baroreceptor reflex is activated when blood pressure drops." |
| Exemplifying | "For example, like in cardiovascular module, if we have a hypotension, the baroreceptor reflex will be activated." |
| Explaining | "The motor system executes the actions we want to perform." |
| Exemplifying | "We can kick, we can punch, we can walk — things like this." |

Key rule: Explicit signals like "for example," "like," or a list of concrete instances → Exemplifying. A standalone factual statement → Explaining.

---

### Pair 4 — Explaining vs. Chronicling
The difference: Explaining describes how or why something works in general. Chronicling narrates the specific sequence of events for a particular patient or clinical case over time.

| Label | Utterance |
|---|---|
| Explaining | "Increased intracranial pressure leads to herniation and brainstem compression." |
| Chronicling | "The patient first developed headache, then lost vision, and then became unable to move." |
| Explaining | "Pyramidal lesions cause contralateral weakness and upper motor neuron signs." |
| Chronicling | "The blood pressure was 180 over 100, and the neurological examination showed flaccid weakness on the right side." |

Key rule: Specific patient + time-ordered events = Chronicling. General mechanism or rule = Explaining.

---

### Pair 5 — Explaining vs. Directing
The difference: Explaining answers "what is it?" or "why does it happen?" Directing answers "what should you do?" or "how do you do it?"

| Label | Utterance |
|---|---|
| Explaining | "Repetitive nerve stimulation measures the amplitude of muscle contraction." |
| Directing | "To test for fatiguability, perform repetitive nerve stimulation at 3–5 Hz." |
| Explaining | "Young patients with stroke have a higher risk of underlying structural lesions." |
| Directing | "You should refer young stroke patients to a neurologist." |

Key rule: Describing a fact or mechanism → Explaining. Telling someone to take an action or follow steps → Directing.

---

### Pair 6 — Managing vs. Facilitating
The difference: Managing controls classroom behavior and logistics. Facilitating poses content questions and seeks student engagement with the subject matter.

| Label | Utterance |
|---|---|
| Managing | "Alright guys, let's start the next lecture." |
| Facilitating | "What is the feature of pyramidal weakness?" |
| Managing | "Please go to www.menti.com and use this code." |
| Facilitating | "The question is: where is the lesion?" |

Key rule: If the utterance is about content knowledge → Facilitating. If it is about participation, logistics, or classroom behavior → Managing.

---

### Pair 7 — Affirming vs. Critiquing
The difference: Affirming confirms the student was correct. Critiquing signals the student was wrong or incomplete.

| Label | Utterance |
|---|---|
| Affirming | "Yes, you are correct." |
| Critiquing | "Not quite correct." |
| Affirming | "You got the point." |
| Critiquing | "Your diagnosis is not correct, because it is missing a very important factor." |

Key rule: Positive confirmation → Affirming. Rejection or correction → Critiquing.

---

### Pair 8 — Affirming vs. Explaining
The difference: Affirming validates a student's answer (response to student). Explaining delivers new factual content (not in response to a student).

| Label | Utterance |
|---|---|
| Affirming | "Considering by mechanism, I think we can call it hypersensitivity." (said after a student's answer) |
| Explaining | "Hypersensitivity is a mechanism by which the immune system overreacts to a stimulus." (unprompted lecture statement) |

Key rule: If the utterance is the teacher's reaction to something a student just said → likely Affirming or Critiquing. If it is an unprompted lecture statement → Explaining.

---

## Utterance to Classify

{utterance}

---

## Instructions

1. Identify which contrastive pair(s) the utterance most resembles.
2. Apply the key rule for that pair to determine which side it belongs on.
3. Select the single best-fitting category.
4. Respond in the following JSON format only — no additional text:

{{
  "label": "<category name>",
  "reasoning": "<one or two sentences. Reference the relevant contrastive pair or key rule if applicable.>"
}}
```

---

## Notes for Python Integration

- Replace `{utterance}` with the actual teacher utterance at runtime.
- The double braces `{{` and `}}` in the JSON output block are escaped for Python's `str.format()` — use `.format(utterance=...)` to fill in the variable.
- If using an f-string instead, change `{{` / `}}` back to `{` / `}` in the JSON block.
- Expected output fields: `label` (one of the 9 class names exactly as written), `reasoning` (free text).
- The 8 pairs target boundaries identified from annotator disagreement in the dataset. Pairs 2–5 cover the Explaining cluster, which is the largest and most frequently confused group.
