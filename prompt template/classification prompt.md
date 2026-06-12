# Prompt 2: Speech Act Classification from Transcript Table

I uploaded or pasted a transcript table from a classroom lecture.

Each row contains one teacher sentence with timestamps.

Your task is to classify each sentence into exactly **one speech act category**.

## Input Columns

The input table should contain these columns:

| index | start_time | end_time | sentence |
| ----- | ---------- | -------- | -------- |

## Output Columns

Create an Excel-compatible table with exactly these columns:

| index | start_time | end_time | sentence | speech_act_label | reasoning |
| ----- | ---------- | -------- | -------- | ---------------- | --------- |

Do not change the original `index`, `start_time`, `end_time`, or `sentence`.

Only add:

1. `speech_act_label`
2. `reasoning`

## Speech Act Labels

Choose exactly one label from this list:

1. Managing
2. Facilitating
3. Using Metadiscourse
4. Chronicling
5. Explaining
6. Exemplifying
7. Directing
8. Critiquing
9. Affirming

Do not create new labels.

---

# Speech Act Category Definitions

## Managing

Utterances used to build, maintain, or manage classroom interaction and teacher-student relationships. These are not mainly about lesson content. They include greetings, jokes, encouragement, classroom instructions, or directives that organize student behavior and participation.

Examples:

* "Alright, alright, alright guys, so, let's start the next lecture."
* "Alright so please go to [www.menti.com](http://www.menti.com) and use this code."
* "I really enjoyed reading your homework reflections, and I'm looking forward to hearing more of your ideas in today's discussion."

## Facilitating

Utterances that ask questions, prompt student participation, or encourage students to consider different perspectives. These usually seek a response from students.

Examples:

* "So what is the motor cortex?"
* "What is the feature of pyramidal weakness?"
* "According to the CDC, what is the incubation period for this disease?"

## Using Metadiscourse

Utterances that organize, frame, repair, or comment on the lecture itself. These include topic transitions, lecture outlines, signals of importance, or statements that clarify lecture structure.

Examples:

* "And for this week, we'll focus on the voluntary motor system."
* "And now, let's move to the next subtopic here, which is the motor cortex."
* "Alright, so that's the introduction of the topic."

## Chronicling

Utterances that describe a patient's clinical history, disease progression, or sequence of events in temporal, causal, or biological order.

Examples:

* "You see the patient come with the sudden onset."
* "The patient presented with right hemiparesis for 20 minutes, and his friend told him that his face was asymmetric and his voice changed."
* "From the physical examination, the blood pressure was quite high, 180 over 100 mmHg, and the neurological examination showed motor weakness on the right side."

## Explaining

Utterances that present factual information, clarify concepts, describe mechanisms, classify phenomena, or explain cause-effect relationships.

Examples:

* "The sensory system is like for the sensing environment."
* "And the motor system is like to execute something that we want to do."
* "Smoking can lead to lung damage and increase the risk of cancer."

## Exemplifying

Utterances that provide examples to illustrate an idea, concept, condition, or application.

Examples:

* "For example, you see the crosswalk ahead, it is a sensing from the environment right?"
* "For example, high temperature is one symptom we should look out for."
* "Another example — like in the cardiovascular module, if we have a hypotension, the baroreceptor reflex will be activated."

## Directing

Utterances that instruct students on how to carry out a method, follow a protocol, or perform a procedure.

Examples:

* "To test for fatiguability, we can test about this by doing the repetitive nerve stimulation."
* "You should refer to the neurologist, especially when the patient is very young."
* "First, sanitize your hands, then put on sterile gloves before touching the wound."

## Critiquing

Utterances that correct, challenge, or disagree with a student's response.

Examples:

* "Not quite correct."
* "Your diagnosis is not correct, because it is missing a very important factor."

## Affirming

Utterances that agree with, confirm, or positively acknowledge a student's response.

Examples:

* "Yes, so, so I think you're right."
* "You got the point."
* "Yes, you are correct."

---

# Classification Rules

Follow these rules carefully:

1. Classify each sentence independently.
2. Choose exactly one speech act label.
3. Do not create new labels.
4. Use the sentence’s main function, not only keywords.
5. If a sentence both explains content and gives an example, choose `Exemplifying` only if the main purpose is to give an example.
6. If a sentence asks students a question, usually choose `Facilitating`.
7. If a sentence organizes the lecture, choose `Using Metadiscourse`.
8. If a sentence gives factual lesson content, choose `Explaining`.
9. If a sentence gives procedural instruction, choose `Directing`.
10. If a sentence describes a patient case over time, choose `Chronicling`.
11. If a sentence corrects or disagrees with a student, choose `Critiquing`.
12. If a sentence confirms or praises a student response, choose `Affirming`.

## Reasoning Column

For the `reasoning` column, write one short reason explaining why the label was chosen.

Keep the reasoning concise.

Example:

```text
The sentence asks students to answer a content question.
```

## Final Output Format

Create a downloadable `.xlsx` file.

If you cannot create a downloadable Excel file, output the result as CSV using this exact column order:

```csv
index,start_time,end_time,sentence,speech_act_label,reasoning
```

Do not include extra explanation before or after the final table.
