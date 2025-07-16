# qualgent-challenge
Backend and CLI tool for QualGent challenge
# QualGent Backend Coding Challenge

## Overview

This project implements a CLI tool and backend service for managing and scheduling AppWright end-to-end test jobs across devices and environments. It also includes a GitHub Actions workflow for continuous integration.

---

## Features

- **CLI tool (`qgjob`)** to submit test jobs and check job status.
- **Backend service** that queues jobs, groups them by `app_version_id` to minimize installs, schedules jobs to available agents, and tracks job status.
- **GitHub Actions integration** to run tests automatically on push, polling job status and failing builds on test failures.

---

## Technology Stack

- Language: Python (can be replaced with Go, Rust, Node.js as desired)
- Backend: FastAPI (REST API)
- Queue: In-memory store / can be configured to Redis or PostgreSQL
- CI: GitHub Actions
- Other tools: Uvicorn (ASGI server)

---

## Setup Instructions

1. **Clone the repository**

```bash
git clone <repo-url>
cd <repo-folder>
