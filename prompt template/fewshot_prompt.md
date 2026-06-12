# Few-Shot LLM-as-a-Judge Prompt Template
# Speech Act Classification

---

## Prompt

```
You are an expert educational discourse analyst. Your task is to classify a teacher's utterance into exactly one speech act category based on the definitions and examples provided below.

---

## Speech Act Categories and Examples

**Managing**
Utterances used to build, maintain, or manage classroom interaction and teacher-student relationships. These are not about lesson content — they include greetings, jokes, encouragement, classroom instructions, or directives that organize student behavior and participation.

Examples:
- "Alright, alright, alright guys, so, let's start the next lecture."
- "Alright so please go to www.menti.com and use this code."
- "I really enjoyed reading your homework reflections, and I'm looking forward to hearing more of your ideas in today's discussion."

---

**Facilitating**
Utterances that ask questions, prompt student participation, or encourage students to consider different perspectives. These typically seek responses from students, especially for formative learning or thematic development.

Examples:
- "So what is the motor cortex?"
- "What is the feature of pyramidal weakness?"
- "According to the CDC, what is the incubation period for this disease?"

---

**Using Metadiscourse**
Utterances that organize, frame, repair, or comment on the lecture itself. These include discourse markers, topic transitions, lecture outlines, signals of importance, or statements that clarify lecture structure — they guide how students follow the lecture rather than delivering new content.

Examples:
- "And for this week, we'll focus on the voluntary motor system."
- "And now, let's move to the next subtopic here, which is the motor cortex."
- "Alright, so that's the introduction of the topic."

---

**Chronicling**
Utterances that describe a patient's clinical history, disease progression, or sequence of events in temporal, causal, or biological order — such as how symptoms developed or how a case unfolded over time.

Examples:
- "You see the patient come with the sudden onset."
- "The patient presented with right hemiparesis for 20 minutes, and his friend told him that his face was asymmetric and his voice changed."
- "From the physical examination, the blood pressure was quite high, 180 over 100 mmHg, and the neurological examination showed motor weakness on the right side."

---

**Explaining**
Utterances that present factual information, clarify concepts, describe mechanisms, classify phenomena, or explain cause-effect relationships — helping students understand what something is, how it works, or why it happens.

Examples:
- "The sensory system is like for the sensing environment."
- "And the motor system is like to execute something that we want to do."
- "Smoking can lead to lung damage and increase the risk of cancer."

---

**Exemplifying**
Utterances that provide examples to illustrate an idea, concept, condition, or application — making abstract or general content more concrete and accessible.

Examples:
- "For example, you see the crosswalk ahead, it is a sensing from the environment right?"
- "For example, high temperature is one symptom we should look out for."
- "Another example — like in the cardiovascular module, if we have a hypotension, the baroreceptor reflex will be activated."

---

**Directing**
Utterances that instruct students on how to carry out a method, follow a protocol, or perform a procedure — often describing ordered steps or providing practical guidance.

Examples:
- "To test for fatiguability, we can test about this by doing the repetitive nerve stimulation."
- "You should refer to the neurologist, especially when the patient is very young."
- "First, sanitize your hands, then put on sterile gloves before touching the wound."

---

**Critiquing**
Utterances that correct, challenge, or disagree with a student's response — pointing out errors, explaining why an answer is incomplete or incorrect, and guiding students toward better understanding.

Examples:
- "Not quite correct."
- "Your diagnosis is not correct, because it is missing a very important factor."

---

**Affirming**
Utterances that agree with, confirm, or positively acknowledge a student's response — indicating that the student's answer or contribution is correct or acceptable.

Examples:
- "Yes, so, so I think you're right."
- "You got the point."
- "Yes, you are correct."

---

## Utterance to Classify

{utterance}

---

## Instructions

1. Read the utterance carefully.
2. Identify which single category best fits based on the definitions and examples above.
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
- Note: **Critiquing** has very few confirmed examples in the dataset — the model may need extra guidance or a fallback rule for this class.
