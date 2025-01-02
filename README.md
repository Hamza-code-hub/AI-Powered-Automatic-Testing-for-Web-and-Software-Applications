# Testing Agent Demo

<p align="center">
  <img src="assets/testing-agent-hero.png" alt="Testing Agent Demo — AI-powered automated testing" width="100%" />
</p>

<p align="center">
  <strong>AI-powered automated testing for web and software applications</strong><br/>
  Turn natural-language test cases into real browser interactions using OpenAI Computer Use and Playwright.
</p>

<p align="center">
  <a href="#overview">Overview</a> •
  <a href="#architecture--execution-flow">Architecture</a> •
  <a href="#core-components">Components</a> •
  <a href="#quick-start">Quick Start</a> •
  <a href="#customization">Customization</a> •
  <a href="#security-notes">Security</a> •
  <a href="#license">License</a>
</p>

<p align="center">
  <img src="https://img.shields.io/badge/License-MIT-2ea44f?style=flat-square" alt="MIT License" />
  <img src="https://img.shields.io/badge/OpenAI-Computer%20Use-111827?style=flat-square" alt="OpenAI Computer Use" />
  <img src="https://img.shields.io/badge/Playwright-Browser%20Automation-45ba63?style=flat-square" alt="Playwright" />
  <img src="https://img.shields.io/badge/Next.js-Frontend-000000?style=flat-square" alt="Next.js" />
  <img src="https://img.shields.io/badge/Node.js-Orchestration-339933?style=flat-square" alt="Node.js" />
  <img src="https://img.shields.io/badge/TypeScript-3178C6?style=flat-square" alt="TypeScript" />
</p>

---

## Overview

**Testing Agent Demo** is a monorepo for AI-assisted frontend testing. It combines an OpenAI Computer Use agent with Playwright browser automation so a user can describe a test in natural language, run it against a web application, and observe the execution from a dedicated frontend.

The project contains three applications that work together:

- **`frontend/`** — Next.js interface for configuring tests and watching them run.
- **`cua-server/`** — Node.js service that communicates with the OpenAI Computer Use model and drives Playwright.
- **`sample-test-app/`** — Example e-commerce application used as a safe target for the demo.

The sample application is included for demonstration only. The reusable automation core lives in the **CUA server + Playwright execution path**.

---

## What This Project Demonstrates

| Capability | Description |
|---|---|
| **Natural-language testing** | Describe a browser test as plain-language instructions instead of manually scripting every interaction. |
| **Real browser execution** | Playwright controls an actual browser and interacts with the target interface. |
| **AI-driven actions** | The Computer Use model interprets the test case and determines the next UI action. |
| **Live execution visibility** | The frontend can be used to configure a test and observe the run. |
| **Reusable automation core** | The CUA server can be adapted to test other web applications. |
| **Safe demo environment** | The included sample e-commerce app provides a controlled target for evaluation. |

---

## Architecture & Execution Flow

<p align="center">
  <img src="assets/testing-agent-architecture-flow.png" alt="Testing Agent architecture and execution flow" width="100%" />
</p>

The end-to-end request flow is:

1. The user writes a **natural-language test case**.
2. The **Next.js frontend** submits the test and target configuration.
3. The **CUA server** coordinates the OpenAI Computer Use model and Playwright.
4. **Playwright** launches or controls the browser.
5. The browser interacts with the **target application**.
6. Execution status and results are returned to the frontend.

A typical test might look like:

```text
Open the login page, enter the demo credentials,
search for a product, add it to the cart,
complete checkout, and verify the success state.
```

The agent interprets that goal and performs the required browser actions until the scenario is complete or execution stops.

---

## Core Components

<p align="center">
  <img src="assets/testing-agent-monorepo-overview.png" alt="Testing Agent monorepo structure and core components" width="100%" />
</p>

### `frontend/`

The frontend provides the operator-facing test interface.

Typical responsibilities include:

- target URL configuration
- natural-language test input
- starting test runs
- watching execution progress
- presenting status and results

### `cua-server/`

The CUA server contains the core testing-agent orchestration.

It is responsible for:

- receiving test instructions
- communicating with the OpenAI Computer Use model
- controlling Playwright browser execution
- coordinating iterative UI actions
- returning execution updates to the frontend

### `sample-test-app/`

The sample application is an example e-commerce web app used as the target under test.

It allows the agent to exercise workflows such as:

- authentication
- navigation
- product discovery
- cart interaction
- checkout-style flows
- interface validation

---

## Repository Layout

```text
AI-Powered-Automatic-Testing-for-Web-and-Software-Applications/
├── frontend/                 # Next.js test configuration and monitoring UI
├── cua-server/               # OpenAI Computer Use + Playwright orchestration
├── sample-test-app/          # Example e-commerce target application
├── docs/
│   └── assets/               # README diagrams and visual assets
├── README.md
└── ...
```

---

## Technology Stack

| Layer | Technology |
|---|---|
| **AI Agent** | OpenAI Computer Use |
| **Browser Automation** | Playwright |
| **Frontend** | Next.js |
| **Server / Orchestration** | Node.js |
| **Language** | TypeScript / JavaScript |
| **Package Management** | npm |
| **Target Application** | Example web application included in the monorepo |

---

## Quick Start

### 1. Clone the repository

```bash
git clone https://github.com/Hamza-code-hub/AI-Powered-Automatic-Testing-for-Web-and-Software-Applications.git
cd AI-Powered-Automatic-Testing-for-Web-and-Software-Applications
```

### 2. Prepare environment files

If `OPENAI_API_KEY` is not already configured in your shell or system environment, create the development environment files:

```bash
cp frontend/.env.example frontend/.env.development
cp cua-server/.env.example cua-server/.env.development
cp sample-test-app/.env.example sample-test-app/.env.development
```

Add your OpenAI API key where required.

The sample application also defines demo credentials:

```env
ADMIN_USERNAME=test_user_name
ADMIN_PASSWORD=test_password
```

Ensure the sample application's development environment contains the expected demo values.

### 3. Install dependencies

```bash
npm install
npx playwright install
```

### 4. Start all applications

```bash
npm run dev
```

---

## Local Services

After startup, the demo exposes three local services:

| Service | Address | Role |
|---|---|---|
| **Frontend UI** | `http://localhost:3000` | Configure tests and observe runs |
| **Sample Test App** | `http://localhost:3005` | Example application under test |
| **CUA Server** | `ws://localhost:8080` | Agent/browser orchestration service |

Open:

```text
http://localhost:3000
```

to access the testing interface.

---

## Example Workflow

A typical run follows this sequence:

```text
Test Case
   ↓
Frontend Configuration
   ↓
CUA Server
   ↓
OpenAI Computer Use
   ↓
Playwright Browser Automation
   ↓
Target Web Application
   ↓
Execution Status / Results
```

Example test case:

```text
Log in with the demo account, navigate to the product catalog,
open a product, add it to the cart, and verify the cart contains the item.
```

This approach lets the test describe **what should happen**, while the agent determines **how to interact with the current interface**.

---

## Customization

The demo can be adapted to another web application by changing the test case and target URL.

You can configure these through the frontend UI or update the project's default values in:

```text
frontend/lib/constants.ts
```

Common extension points include:

- custom test scenarios
- different target applications
- additional browser workflows
- enhanced test-result reporting
- screenshots and execution artifacts
- test-history persistence
- CI/staging integration
- application-specific safety constraints

The `sample-test-app` is only an example. For integration into another system, the most important reusable component is the **`cua-server` orchestration layer**.

---

## Intended Use

This project is best suited for:

- AI-assisted QA experimentation
- frontend regression testing in controlled environments
- browser workflow validation
- staging-environment test automation
- evaluating natural-language test execution
- prototyping agentic software-testing workflows

It is a demonstration of how an AI agent can connect **test intent** to **real interface interaction**.

---

## Security Notes

> [!CAUTION]
> Use this project only in controlled test or evaluation environments.

Computer-use agents can make incorrect decisions, misinterpret interface state, or perform unintended actions. Do not assume that an AI-controlled browser has the same safety guarantees as a deterministic test script.

Recommended precautions:

- test only systems you own or are explicitly authorized to test
- use isolated development or staging environments
- do not use real customer or production data
- do not expose production credentials to the agent
- avoid high-stakes or irreversible workflows
- constrain the agent to the intended target application and test scope
- review test behavior before expanding automation privileges

---

## Project Scope

This repository focuses on demonstrating the core agentic testing workflow:

```text
Natural-language intent
        ↓
AI interpretation
        ↓
Browser interaction
        ↓
Application validation
        ↓
Visible test result
```

It is not intended to replace a complete deterministic QA strategy. Traditional unit, integration, API, and deterministic end-to-end tests remain useful alongside agent-driven testing.

---

## License

This project is licensed under the **MIT License**.

See the repository's `LICENSE` file for details.

---

<p align="center">
  <strong>Describe the test. Let the agent run it. Observe the result.</strong>
</p>
