# Centralized GitHub Actions & Workflows

This repository contains reusable GitHub Actions workflows (`workflow_call`) used across all `@Noahffiliation` projects.

---

## Reusable Workflows

| Workflow | Description | Path |
| :--- | :--- | :--- |
| **Node.js CI/CD** | Lint (Prettier/ESLint), TypeScript, Tests + Coverage, SonarCloud, Next.js Caching, Bundle Build | [`.github/workflows/reusable-node-ci.yml`](.github/workflows/reusable-node-ci.yml) |
| **Python CI/CD** | Ruff (lint & format), Mypy, Pytest + Coverage, SonarCloud, Docker build validation | [`.github/workflows/reusable-python-ci.yml`](.github/workflows/reusable-python-ci.yml) |
| **Android CI/CD** | JDK 21, Spotless, Android Lint (SARIF), JUnit + JaCoCo, SonarCloud, Debug APK | [`.github/workflows/reusable-android-ci.yml`](.github/workflows/reusable-android-ci.yml) |
| **CodeQL SAST** | CodeQL Security Analysis uploading SARIF to GitHub Security tab | [`.github/workflows/reusable-codeql.yml`](.github/workflows/reusable-codeql.yml) |

---

## How to Use

### 1. Node.js / Web Apps
Create `.github/workflows/ci.yml`:
```yaml
name: CI

on:
  push:
    branches: [main, develop]
  pull_request:
    branches: [main]

jobs:
  node-ci:
    uses: Noahffiliation/.github/.github/workflows/reusable-node-ci.yml@main
    with:
      node-version: "24.19.0"
      run-build: true
      build-output-dir: "dist" # Or .next, out, build
    secrets: inherit
```

---

### 2. Python Automation & Data Syncs
Create `.github/workflows/ci.yml`:
```yaml
name: CI

on:
  push:
    branches: [main]
  pull_request:
    branches: [main]

jobs:
  python-ci:
    uses: Noahffiliation/.github/.github/workflows/reusable-python-ci.yml@main
    with:
      python-version: "3.12.3"
      test-docker: true
    secrets: inherit
```

---

### 3. Android Mobile
Create `.github/workflows/ci.yml`:
```yaml
name: CI

on:
  push:
    branches: [main]
  pull_request:
    branches: [main]

jobs:
  android-ci:
    uses: Noahffiliation/.github/.github/workflows/reusable-android-ci.yml@main
    with:
      java-version: "21"
    secrets: inherit
```

---

### 4. CodeQL Security Analysis
Create `.github/workflows/codeql.yml`:
```yaml
name: "CodeQL Security"

on:
  push:
    branches: [main]
  pull_request:
    branches: [main]
  schedule:
    - cron: '17 3 * * 1'

jobs:
  security-scan:
    uses: Noahffiliation/.github/.github/workflows/reusable-codeql.yml@main
    with:
      language: "python" # Or 'javascript-typescript', 'java-kotlin'
```
