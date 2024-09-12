# Shared Workflows for GitHub Actions

This repository contains shared workflows for GitHub Actions that are designed to streamline common tasks such as setting up environments, building, and testing applications.

## Overview

Shared workflows are reusable configurations for GitHub Actions that help automate and standardize processes across multiple projects. This repository includes a shared workflow for setting up a Node.js environment.

## Available Workflows

### 1. Setup Node.js Environment

**File:** `.github/workflows/setup-node.yml`

**Description:** This workflow sets up a Node.js environment with a specified or default version. It is useful for ensuring that all projects use a consistent Node.js version.

**Usage:**

To use this workflow in another repository, create a new workflow file in the `.github/workflows` directory of that repository and include the following configuration:

```yaml
name: CI

on:
  push:
    branches:
      - main
  pull_request:
    branches:
      - main

jobs:
  setup-node:
    uses: <your-repo>/path/to/.github/workflows/setup-node.yml@main
    with:
      node-version: "20.17.0" # Optional: Specify the Node.js version you want to use
```

### 2. Cache and Install Dependencies

**File:** `.github/workflows/cache-install-dependencies.yml`

**Description:** This workflow caches Node.js modules to speed up dependency installation and ensures that dependencies are installed consistently based on a specified lock file.

**Usage:**

To use this workflow in another repository, create a new workflow file in the `.github/workflows` directory of that repository and include the following configuration:

```yaml
name: CI

on:
  push:
    branches:
      - main
  pull_request:
    branches:
      - main

jobs:
  cache-install-dependencies:
    uses: <your-repo>/path/to/.github/workflows/cache-install-dependencies.yml@main
    with:
      node-version: "20.17.0" # Optional: Specify the Node.js version
      lock-file: "package-lock.json" # Optional: Specify the lock file path
      cache-path: "server/node_modules" # Optional: Specify the cache file path
      cache-key-prefix: "server-node" # Optional: Specify the cache key name
      working-directory: "server"
```

### 3 Security Audit

**File:** `.github/workflows/security-audit.yml`

**Description:** This workflow performs a security audit of the project, using npm audit by default, and provides flexibility for other audit or security-related commands. It also caches Node.js modules based on the lock file and provides options to continue the workflow on error or stop.

**Usage:**

To use this workflow in another repository, create a new workflow file in the `.github/workflows` directory of that repository and include the following configuration:

```yaml
name: CI

on:
  push:
    branches:
      - main
  pull_request:
    branches:
      - main

jobs:
  cache-install-dependencies:
    uses: <your-repo>/path/to/.github/workflows/security-audit.yml@main
    with:
      node-version: 'latest' # Specify the Node version
      lock-file: 'package-lock.json' # Specify the lock file for caching
      cache-path: 'node_modules' # Specify the cache directory
      cache-key-prefix: 'node' # Specify cache key prefix
      continue-on-error: true # Specify whether to continue on error
      run-cmd: 'npm audit --audit-level=high' # Specify the command to run for auditing
      working-directory: 'server' # Specify the working directory
```
