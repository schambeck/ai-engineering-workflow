You are an expert software architect and technical writer.

Your task is to analyze the current project repository and generate a complete, high-quality README.md file based on the actual codebase, structure, and detected technologies.

## 🔍 Analysis Instructions

1. Inspect the entire repository, including:

    * Folder structure
    * Source code files
    * Configuration files (e.g., package.json, pom.xml, docker-compose.yml, etc.)
    * Environment variables and settings
    * Existing documentation (if any)

2. Automatically infer:

    * Project purpose and domain
    * Main features and functionalities
    * Tech stack (languages, frameworks, libraries)
    * Architecture patterns (e.g., monolith, microservices, server-driven UI, etc.)
    * Key modules and responsibilities
    * External dependencies and integrations
    * Build and run process

3. If the project context is unclear, make the most reasonable assumption based on the code.

---

## 🧱 README Structure to Generate

Produce a clean, professional README.md with the following sections:

### 1. Title

* Use the project name (or infer from repo)

### 2. Description

* Concise explanation of what the project does
* Include the problem it solves and its value

### 3. Architecture Overview

* Describe the system design at a high level
* Mention patterns and design decisions

### 4. Features

* List main functionalities
* Group them logically if needed

### 5. Tech Stack

* Backend
* Frontend (if applicable)
* Infrastructure / DevOps
* Database

### 6. Project Structure

* Explain key folders and their responsibilities

### 7. Getting Started

* Prerequisites
* Installation steps
* How to run locally

### 8. Usage

* How to use the system
* Example flows or commands

### 9. API (if applicable)

* Main endpoints or interaction model

### 10. Configuration

* Environment variables
* Important configs

### 11. Deployment

* How to deploy (Docker, cloud, etc.)

### 12. Contributing

* Guidelines for contributing

### 13. License

* Add a placeholder if not found

---

## ✨ Writing Guidelines

* Be clear, concise, and technical
* Avoid generic descriptions — base everything on real code evidence
* Use markdown best practices
* Use code blocks where appropriate
* Use diagrams (e.g., mermaid) if architecture is complex

---

## ⚠️ Constraints

* Do NOT hallucinate features that do not exist
* If something is uncertain, indicate assumptions clearly
* Prioritize accuracy over verbosity

---

## 🎯 Output

Return ONLY the final README.md content, fully formatted in Markdown.
