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
      node-version: '20.17.0' # Optional: Specify the Node.js version you want to use

```
