# GitHub Actions Deployment Guide

This repository contains GitHub Actions workflows for automated deployment to three environments: DEV, TEST, and PROD.

## Overview

The OGSurvival network runs in isolated containers across three environments, each with their own secrets, ports, and configurations:

- **DEV**: Latest unstable code from dev branches - for internal testing
- **TEST**: Tested code and new features - for community testing
- **PROD**: Latest stable version - for normal players

## Workflows

### 1. DEV Environment (`dev-deploy.yml`)

**Triggers:**
- Push to `dev`, `develop`, or `dev/**` branches
- Manual dispatch

**Features:**
- Builds and pushes Docker images to GitHub Container Registry
- Deploys latest unstable code for internal testing
- Uses `dev` environment configuration

### 2. TEST Environment (`test-deploy.yml`)

**Triggers:**
- Push to `test`, `testing`, or `test/**` branches
- Pre-release creation
- Manual dispatch

**Features:**
- Builds and pushes Docker images with test tags
- Runs integration tests
- Uses `test` environment configuration
- Suitable for community testing

### 3. PROD Environment (`prod-deploy.yml`)

**Triggers:**
- Push to `main` or `master` branches
- Release creation
- Manual dispatch

**Features:**
- Builds and pushes production-ready Docker images
- Includes pre and post-deployment validation
- Uses `production` environment configuration
- Semantic versioning support

## Environment Configuration

Each environment requires specific setup in GitHub repository settings:

### Environment Variables

Configure the following variables for each environment:

#### DEV Environment
- `DEV_HOST`: Development server hostname
- `DEV_PORT`: Development server port

#### TEST Environment
- `TEST_HOST`: Test server hostname
- `TEST_PORT`: Test server port

#### PROD Environment
- `PROD_HOST`: Production server hostname
- `PROD_PORT`: Production server port

### Environment Secrets

Configure the following secrets for each environment:

#### DEV Environment
- `DEV_DATABASE_URL`: Development database connection string
- `DEV_API_KEY`: Development API key
- Additional environment-specific secrets

#### TEST Environment
- `TEST_DATABASE_URL`: Test database connection string
- `TEST_API_KEY`: Test API key
- Additional environment-specific secrets

#### PROD Environment
- `PROD_DATABASE_URL`: Production database connection string
- `PROD_API_KEY`: Production API key
- Additional environment-specific secrets

## Setting Up Environments

1. Go to repository Settings → Environments
2. Create three environments: `dev`, `test`, `production`
3. Configure environment variables and secrets for each
4. Set up environment protection rules as needed:
   - **DEV**: No restrictions
   - **TEST**: Require reviewers for sensitive changes
   - **PROD**: Require reviewers and wait timers

## Docker Image Management

All images are stored in GitHub Container Registry (`ghcr.io`) with the following tagging strategy:

- **DEV**: `dev-latest`, `dev-{sha}`
- **TEST**: `test-latest`, `test-{sha}`
- **PROD**: `latest`, `{version}`, `{major}.{minor}`

## Deployment Process

### Development Workflow
1. Push code to dev branch
2. Automatic build and deployment to DEV environment
3. Internal testing and validation

### Testing Workflow
1. Push tested code to test branch or create pre-release
2. Automatic build and deployment to TEST environment
3. Integration tests run automatically
4. Community testing and feedback

### Production Workflow
1. Push to main/master or create release
2. Pre-deployment checks run
3. Automatic build and deployment to PROD environment
4. Post-deployment validation
5. Production monitoring

## Customization

To customize the workflows for your specific needs:

1. **Dockerfile**: Ensure your repository has a `Dockerfile` in the root
2. **Deployment Commands**: Replace example commands in the workflows with your actual deployment logic
3. **Tests**: Add your integration and validation tests
4. **Notifications**: Configure notifications (Slack, Discord, etc.)

## Security Considerations

- Use GitHub environments to manage secrets securely
- Implement proper access controls and reviews
- Monitor deployment logs and activities
- Use least privilege principle for service accounts
- Regular security audits of deployment processes

## Troubleshooting

### Common Issues

1. **Docker Build Failures**: Ensure Dockerfile exists and is valid
2. **Registry Access**: Verify GitHub token permissions
3. **Environment Variables**: Check environment configuration
4. **Deployment Timeouts**: Increase timeout values if needed

### Debugging

- Check workflow logs in GitHub Actions tab
- Verify environment variables and secrets
- Test deployment commands locally
- Review container logs after deployment

## Support

For issues or questions:
1. Check workflow logs first
2. Review environment configuration
3. Create an issue in this repository
4. Contact the development team

---

*This documentation should be updated as the deployment process evolves.*