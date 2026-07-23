# Employee Training Automation

This branch contains the workflow automation responsible for managing the employee training lifecycle before quiz submission.

The implementation consists of two integrated workflows:

- **Flow 1 – Training Auto Assignment**
- **Flow 2 – Quiz Release & Reminder**

Together, these workflows automate the process of assigning mandatory training, distributing learning materials, releasing quizzes, and reminding employees until the assignment reaches completion or expires.

---

## Workflow Overview

```
Employees
      │
      ▼
Role Matching
      │
      ▼
Training Assignment
      │
      ▼
Training Email
      │
      ▼
Learning Period (7 Days)
      │
      ▼
Quiz Release
      │
      ▼
Reminder Automation
      │
      ▼
Assignment Completed
        │
        ├──────────────► Continue to Quiz Submission Workflow
        │
        └──────────────► Overdue → Failed
```

---

# Flow 1 — Training Auto Assignment

## Objective

Automatically assign mandatory training modules to employees based on their role while preventing duplicate assignments.

---

## Business Process

1. Retrieve all active employees.
2. Retrieve all available training modules.
3. Match employee roles with mandatory training requirements.
4. Check whether an assignment already exists.
5. Create a new training assignment.
6. Send training material via email.
7. Notify HR with the assignment summary.

---

## Workflow

```
Cron Trigger
      │
      ▼
Get Active Employees
      │
      ▼
Get Training Modules
      │
      ▼
Role Matching
      │
      ▼
Assignment Exists?
      │
      ├── Yes ─────────► Skip
      │
      └── No
            │
            ▼
Create Assignment
            │
            ▼
Send Training Email
            │
            ▼
Notify HR
```

---

## Functional Requirements

| ID | Description |
|----|-------------|
| FR-1 | Retrieve active employees from the Employees table. |
| FR-2 | Retrieve available training modules. |
| FR-3 | Match employee roles with mandatory training requirements. |
| FR-4 | Prevent duplicate assignments. |
| FR-5 | Create a new training assignment record. |
| FR-6 | Send training assignment email. |
| FR-7 | Notify HR after assignment creation. |

---

## Assignment Data

Each assignment stores the following information.

| Field |
|-------|
| assignment_id |
| employee_id |
| module_id |
| assigned_date |
| due_date |
| status |
| reminder_count |

---

## Output

### Employee Email

Includes:

- Training module
- Learning material
- Due date

### HR Notification

Contains a summary of newly assigned training.

---

# Flow 2 — Quiz Release & Reminder

## Objective

Automatically release quizzes after the learning period and manage reminder notifications until the assignment is completed or overdue.

---

## Business Process

1. Check all active assignments.
2. Wait until the learning period reaches seven days.
3. Release the quiz.
4. Update assignment status.
5. Send reminder emails if the quiz has not been completed.
6. Escalate overdue assignments to HR.

---

## Workflow

```
Cron Trigger
      │
      ▼
Get Active Assignments
      │
      ▼
Learning Period Complete?
      │
      ├── No ─────────► End
      │
      └── Yes
            │
            ▼
Release Quiz
            │
            ▼
Update Status
            │
            ▼
Reminder Engine
            │
            ├── Reminder 1
            ├── Reminder 2
            ├── Reminder 3
            │
            ▼
Due Date Passed?
            │
            ├── No ─────► End
            │
            └── Yes
                  │
                  ▼
Escalate to HR
                  │
                  ▼
Update Status = Failed
```

---

## Reminder Schedule

| Reminder | Condition |
|-----------|-----------|
| Reminder 1 | 3 days after quiz release |
| Reminder 2 | 5 days after quiz release |
| Reminder 3 | 1 day before due date |

---

## Assignment Status

```
Assigned
      │
      ▼
In Progress
      │
      ├────────► Completed
      │
      └────────► Failed
```

---

## Functional Requirements

| ID | Description |
|----|-------------|
| FR-8 | Release quizzes after the learning period. |
| FR-9 | Update assignment status to **In Progress**. |
| FR-10 | Send Reminder 1. |
| FR-11 | Send Reminder 2. |
| FR-12 | Send Reminder 3. |
| FR-13 | Escalate overdue assignments to HR. |
| FR-14 | Mark overdue assignments as **Failed**. |

---

## Reminder State

| Value | Description |
|-------|-------------|
| 0 | No reminder sent |
| 1 | Reminder 1 |
| 2 | Reminder 2 |
| 3 | Final reminder |

---

## Technology Stack

| Category | Technology |
|----------|------------|
| Workflow Engine | n8n |
| Database | Airtable |
| Email | Node Gmail |
| Scheduling | Cron |
| Reporting | Telegram |

---

## Repository Structure

```
training-automation
│
├── README.md
├── flow1-training-auto-assignment.json
└── flow2-quiz-release-reminder.json
```

---

## Notes

This branch covers the automation process from employee assignment until quiz availability.

The final evaluation process, certificate generation, and quiz submission handling are implemented separately in the **quiz-submission** branch.
