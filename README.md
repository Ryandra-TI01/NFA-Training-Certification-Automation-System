# NFA Training & Certification Automation System

An end-to-end workflow automation project developed as the final project for the **AI for Business Independent Study Program** at **NF Academy**.

This project demonstrates how business processes in employee training and certification can be automated using **n8n**, reducing manual administrative work while improving process consistency and operational efficiency.

---

## Overview

The system automates the complete employee training lifecycle, including:

- Automatic training assignment
- Learning material distribution
- Scheduled quiz release
- Reminder automation
- Quiz submission processing
- Certificate generation
- HR reporting

The implementation is separated into multiple workflows to improve maintainability and scalability.

---

## Repository Structure

```
NFA-Training-Certification-Automation-System
│
├── main
│   └── README.md
│
├── training-automation
│   ├── README.md
│   ├── flow1-training-auto-assignment.json
│   └── flow2-quiz-release-reminder.json
│
└── quiz-submission
    ├── README.md
    └── flow3-quiz-submission.json
```

---

## Branches

| Branch | Description |
|----------|-------------|
| `main` | Project overview and repository documentation |
| `training-automation` | Training Auto-Assignment and Quiz Release & Reminder workflows |
| `quiz-submission` | Quiz submission processing, certificate generation, and evaluation workflow |

---

## Technology Stack

| Category | Technology |
|----------|------------|
| Workflow Automation | n8n |
| Database | Airtable |
| Form Submission | Tally |
| Document Generation | PDFMonkey |
| Notification | Email |
| Notification | Telegram |
| Reporting | PDF |

---

## Workflow Summary

### Training Automation

Automates employee training assignments based on role, distributes learning materials, releases quizzes, and manages reminder notifications until completion.

### Quiz Submission

Processes quiz submissions, validates scores, updates training status, generates completion certificates, and delivers evaluation results automatically.

---

## Key Features

- Automated employee training assignment
- Scheduled quiz distribution
- Reminder workflow
- Quiz evaluation
- Automatic certificate generation
- HR reporting
- Workflow orchestration using n8n
- Database integration with Airtable

---

## Project Goals

- Reduce repetitive administrative tasks
- Standardize employee training processes
- Improve monitoring and reporting
- Increase workflow reliability through automation
- Demonstrate practical implementation of business process automation

---

## License

This repository was developed for educational and portfolio purposes as part of the **AI for Business Independent Study Program** at **NF Academy**.

---

## Author

**Ryandra Athaya Saleh**

Software Engineering Student

Backend Development • Workflow Automation • Business Process Automation
