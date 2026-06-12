# Prompt 1: ASR Transcript from Classroom Lecture

I uploaded an audio or video file of a classroom lecture.

Your task is to transcribe **all teacher speech** from the file.

## Output Goal

Create an Excel-compatible table where each row is **one sentence only**.

## Output Columns

Use exactly these columns:

| index | start_time | end_time | sentence |
| ----- | ---------- | -------- | -------- |

Use this timestamp format:

```text
HH:MM:SS
```

Example:

```text
00:03:25
```

## Transcription Rules

Please follow these rules carefully:

1. Extract only teacher speech.
2. Segment the transcript into sentence-level rows.
3. Each row must contain only one sentence.
4. Add approximate `start_time` and `end_time` for each sentence.
5. Preserve medical, classroom, and technical terms as much as possible.
6. Do not summarize.
7. Do not paraphrase.
8. Do not translate unless the teacher switches language.
9. Keep the original language of the utterance.
10. Lightly clean repeated fillers only when they do not change meaning.
11. If timestamps are uncertain, still provide the best approximate start and end time.

## Final Output Format

Create a downloadable `.xlsx` file.

If you cannot create a downloadable Excel file, output the result as CSV using this exact column order:

```csv
index,start_time,end_time,sentence
```

Do not include extra explanation before or after the table.
