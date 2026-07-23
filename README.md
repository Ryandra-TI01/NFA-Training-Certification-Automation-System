# Quiz Submission

This branch contains the workflow responsible for processing employee quiz submissions and automatically generating training certificates.

The workflow is triggered whenever a participant submits a completed quiz through **Tally**. It validates the submission, evaluates the participant's score, updates the training assignment status, generates certificates for successful participants, and sends the final evaluation via email.

---

## Workflow Overview

```
Tally Submission
        │
        ▼
Validate Assignment
        │
        ▼
Retrieve Employee Data
        │
        ▼
Retrieve Training Module
        │
        ▼
Evaluate Quiz Score
        │
        ├──────────────► Failed
        │                    │
        │                    ▼
        │             Update Assignment
        │                    │
        │                    ▼
        │            Send Evaluation Email
        │
        ▼
Passed
        │
        ▼
Generate Certificate
        │
        ▼
Save Certificate URL
        │
        ▼
Update Assignment
        │
        ▼
Send Certificate Email
```

---

# Objective

Automatically process quiz submissions, determine participant eligibility based on the passing score, and issue digital certificates for employees who successfully complete mandatory training.

---

# Business Process

1. Receive quiz submission from Tally.
2. Validate the submitted assignment.
3. Retrieve employee information.
4. Retrieve the associated training module.
5. Compare the participant's score against the module passing score.
6. Update assignment status.
7. Generate a PDF certificate for successful participants.
8. Store the certificate URL.
9. Send the final evaluation email.

---

# Workflow

```
Webhook (Tally)
        │
        ▼
Validate Assignment
        │
        ▼
Load Employee
        │
        ▼
Load Training Module
        │
        ▼
Compare Score
        │
        ├──────────────► Score < Passing Score
        │                    │
        │                    ▼
        │             Update Status = Failed
        │                    │
        │                    ▼
        │            Send Failure Email
        │
        ▼
Score ≥ Passing Score
        │
        ▼
Generate Certificate
        │
        ▼
Upload Certificate
        │
        ▼
Save Certificate URL
        │
        ▼
Update Status = Completed
        │
        ▼
Send Certificate Email
```

---

# Functional Requirements

| ID | Description |
|----|-------------|
| FR-15 | Receive quiz submissions from Tally. |
| FR-16 | Validate the submitted assignment. |
| FR-17 | Retrieve employee, training module, and assignment information. |
| FR-18 | Compare participant score with the module passing score. |
| FR-19 | Mark assignment as **Completed** when the participant passes. |
| FR-20 | Generate a PDF certificate automatically. |
| FR-21 | Store the certificate URL in the assignment record. |
| FR-22 | Send a completion email with the generated certificate. |
| FR-23 | Mark assignment as **Failed** when the participant does not meet the passing score. |
| FR-24 | Send the final evaluation email for unsuccessful participants. |

---

# Assignment State Transition

```
In Progress
      │
      ▼
Quiz Submitted
      │
      ├──────────────► Passed
      │                    │
      │                    ▼
      │              Completed
      │
      └──────────────► Failed
```

---

# Output

## Successful Submission

The workflow performs the following actions:

- Updates assignment status to **Completed**
- Generates a PDF certificate
- Saves the certificate URL
- Sends the certificate via email

---

## Failed Submission

The workflow performs the following actions:

- Updates assignment status to **Failed**
- Records participant score
- Sends an evaluation email

---

# Technology Stack

| Category | Technology |
|----------|------------|
| Workflow Engine | n8n |
| Form Platform | Tally |
| Database | Airtable |
| PDF Generation | PDFMonkey |
| Email | Node Gmail |

---

# Repository Structure

```
quiz-submission
│
├── README.md
└── flow3-quiz-submission.json
```

---

# Integration

This workflow is designed to work together with the **training-automation** branch.

The overall automation process is divided into two stages:

```
training-automation
│
├── Flow 1 — Training Auto Assignment
└── Flow 2 — Quiz Release & Reminder
                │
                ▼
quiz-submission
│
└── Flow 3 — Quiz Submission
        │
        ▼
Certificate Generation
```

---

# Notes

This workflow assumes that:

- Training assignments have already been created.
- Quiz invitations have already been sent.
- Participants access quizzes through Tally.
- Assignment and employee data are stored in Supabase.

The workflow focuses exclusively on submission processing, evaluation, and certificate generation.
