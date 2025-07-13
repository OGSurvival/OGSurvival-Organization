# Example Docker Compose Configuration for OGSurvival Network

This directory contains example Docker Compose configurations for different environments.

## Environment-Specific Configurations

### DEV Environment
- Uses development database
- Debug logging enabled
- Hot reload for development
- Exposed development ports

### TEST Environment
- Uses test database
- Integration testing setup
- Monitoring enabled
- Community access ports

### PROD Environment
- Production database
- Optimized performance
- Full monitoring and logging
- Load balancing ready

## Usage

These are example configurations. Actual deployment should be customized based on your specific services and requirements.

The GitHub Actions workflows can use these configurations for consistent deployments across environments.