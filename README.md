# QualGent Backend Coding Challenge

#Overview

This project implements a CLI tool and backend service for managing and scheduling AppWright end-to-end test jobs across devices and environments. It also includes a GitHub Actions workflow for continuous integration.

---

#Features

- **CLI tool (`qgjob`)** to submit test jobs and check job status.
- **Backend service** that queues jobs, groups them by `app_version_id` to minimize installs, schedules jobs to available agents, and tracks job status.
- **GitHub Actions integration** to run tests automatically on push, polling job status and failing builds on test failures.

---

#Technology Stack

- Language: Python (can be replaced with Go, Rust, Node.js as desired)
- Backend: FastAPI (REST API)
- Queue: In-memory store / can be configured to Redis or PostgreSQL
- CI: GitHub Actions
- Other tools: Uvicorn (ASGI server)

---

#Setup Instructions

1. **Clone the repository**

```bash
git clone <repo-url>
cd <repo-folder>
Create and activate the virtual environment
python3 -m venv .venv
source .venv/bin/activate
Install dependencies
pip install -r requirements.txt
Run the backend server
uvicorn server.main:app --reload
Use the CLI tool
Submit a job:

qgjob submit --org-id=qualgent --app-version-id=xyz123 --test=tests/onboarding.spec.js
Check job status:

qgjob status --job-id=<job-id>

Architecture

The backend service manages job queueing, grouping jobs by app_version_id to optimize test execution.
The CLI communicates with the backend over REST to submit and monitor jobs.
GitHub Actions runs the CLI tool as part of CI, automatically submitting tests and monitoring results.
Simple architecture diagram:

[CLI qgjob] <--> [Backend REST API] <--> [Job Queue & Scheduler] <--> [Test Agents/Devices]
How Grouping and Scheduling Works

Jobs submitted with the same app_version_id are grouped together to run on the same device to reduce app reinstallation overhead.
The backend assigns jobs to available agents based on device availability and target environment (emulator, device, BrowserStack).
Job status and execution progress are tracked and reported through the backend API.
Running End-to-End Test Submission

Start the backend server.
Use the CLI to submit a test job.
Monitor job status via CLI or GitHub Actions workflow.
Review logs and results to confirm test execution.
GitHub Actions Workflow

Defined in .github/workflows/appwright_test.yml.
Runs on push events.
Installs qgjob.
Submits tests.
Polls for completion.
Fails the build if any test fails.
