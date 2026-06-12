# Zero-Shot LLM-as-a-Judge Prompt Template
# Speech Act Classification

---

## Prompt

```
You are an expert educational discourse analyst. Your task is to classify a teacher's utterance into exactly one speech act category based on the definitions provided below.

---

## Speech Act Categories

**Managing**
Utterances used to build, maintain, or manage classroom interaction and teacher-student relationships. These are not about lesson content — they include greetings, jokes, encouragement, classroom instructions, or directives that organize student behavior and participation.

**Facilitating**
Utterances that ask questions, prompt student participation, or encourage students to consider different perspectives. These typically seek responses from students, especially for formative learning or thematic development.

**Using Metadiscourse**
Utterances that organize, frame, repair, or comment on the lecture itself. These include discourse markers, topic transitions, lecture outlines, signals of importance, or statements that clarify lecture structure — they guide how students follow the lecture rather than delivering new content.

**Chronicling**
Utterances that describe a patient's clinical history, disease progression, or sequence of events in temporal, causal, or biological order — such as how symptoms developed or how a case unfolded over time.

**Explaining**
Utterances that present factual information, clarify concepts, describe mechanisms, classify phenomena, or explain cause-effect relationships — helping students understand what something is, how it works, or why it happens.

**Exemplifying**
Utterances that provide examples to illustrate an idea, concept, condition, or application — making abstract or general content more concrete and accessible.

**Directing**
Utterances that instruct students on how to carry out a method, follow a protocol, or perform a procedure — often describing ordered steps or providing practical guidance.

**Critiquing**
Utterances that correct, challenge, or disagree with a student's response — pointing out errors, explaining why an answer is incomplete or incorrect, and guiding students toward better understanding.

**Affirming**
Utterances that agree with, confirm, or positively acknowledge a student's response — indicating that the student's answer or contribution is correct or acceptable.

---

## Utterance to Classify

{utterance}

---

## Instructions

1. Read the utterance carefully.
2. Identify which single category best fits based on the definitions above.
3. Respond in the following JSON format only — no additional text:

{{
  "label": "<category name>",
  "reasoning": "<one or two sentences explaining why this category fits best>"
}}
```

---

## Notes for Python Integration

- Replace `{utterance}` with the actual teacher utterance at runtime.
- The double braces `{{` and `}}` in the JSON output block are escaped for Python's `str.format()` — use `.format(utterance=...)` to fill in the variable.
- If using an f-string instead, change `{{` / `}}` back to `{` / `}` in the JSON block.
- Expected output fields: `label` (one of the 9 class names exactly as written), `reasoning` (free text).
