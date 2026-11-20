# Telegram Student Report Router 🤖📊

An automated backend pipeline built on **n8n** that streamlines student performance processing. It receives PDF scorecards via **Telegram**, extracts critical metrics using a **Groq Chat Model**, routes the output based on examination results, and delivers customized email notifications with the original report attached via **Gmail**.

---

## Architecture Flow

1. **Telegram Trigger**: Ingests incoming PDF performance reports or transcripts sent via chat.
2. **Extract from File**: Parses the raw text content out of the PDF document.
3. **Information Extractor**: Leverages a non-Llama Groq model to extract structured attributes (`student_name`, `student_id`, `course_name`, `final_grade`, `result_status`).
4. **IF Node**: Evaluates `result_status` to split traffic into **Pass** and **Fail** branches.
5. **Gmail Dispatch**: Sends personalized notification emails with the student's score and dynamically attaches the original PDF report (`data`).

---

## Extracted JSON Schema

```json
{
  "student_name": "String",
  "student_id": "String",
  "course_name": "String",
  "final_grade": "Number",
  "result_status": "String (Passed / Failed)"
}
