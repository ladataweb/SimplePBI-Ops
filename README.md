# SimplePBI-Ops GitHub Action

[![GitHub Release](https://img.shields.io/github/v/release/ladataweb/SimplePBI-Ops)](https://github.com/ladataweb/SimplePBI-Ops/releases)

**SimplePBI-Ops** is a GitHub Action that automates the deployment of Power BI projects using the **SimplePBI Python library**.  
It detects changes in your workspaces, handles dependencies, and runs your deployment script automatically — so users only need to provide secrets and trigger the workflow.

## Features

- Fully self-contained “black box” action
- Detects which Semantic Models or Reports have changed
- Runs the Python deployment script automatically
- Handles Python setup and dependency installation
- Minimal setup for end users

## Usage

Create a workflow in your repository (e.g., `.github/workflows/deploy.yml`):

```yaml
name: Deploy PowerBI

on:
  push:
    branches:
      - main
    paths:
      - 'Workspaces/**'   # Trigger only when files in Workspaces/ change

jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - name: Run SimplePBI Ops
        uses: ladataweb/SimplePBI-Ops@v0.0.6
        with:
          tenant_id: ${{ secrets.TENANT_ID }}
          app_id: ${{ secrets.APP_ID }}
          secret_key: ${{ secrets.SECRET_KEY }}
```

## How it works

1. Checkout code: Automatically checks out your repository.
2. Setup Python: Installs Python 3.x and dependencies (simplepbi).
3. Detect changes: Finds which folders in Workspaces/ changed in the latest commit.
4. Run deployment: Calls the included ldw-deploy.py Python script with the list of changed folders and secrets.

## Requirements

- GitHub repository must contain a Workspaces/ folder with .report or .semanticmodel projects.
- Secrets (TENANT_ID, APP_ID, SECRET_KEY) must be configured in the repository’s settings.

## License
License © Ignacio Barrau
