# OGSurvival-Organization
Repository for documentation, issues and discussions

## Overview
This repository contains organizational documentation, issue tracking, and automated deployment workflows for the OGSurvival network.

## GitHub Actions
The repository includes GitHub Actions workflows for automated deployment to three environments:
- **DEV**: Latest unstable code from dev branches for internal testing
- **TEST**: Tested code and new features for community testing
- **PROD**: Latest stable version for normal players

See [`.github/workflows/README.md`](.github/workflows/README.md) for detailed deployment documentation.

## Docker Configuration
Example Docker Compose configurations are provided in the [`docker/`](docker/) directory for consistent containerized deployments across environments.
