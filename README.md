# CAMARA Reporting Workflow

## Purpose

This repository contains an automated GitHub Actions workflow that generates comprehensive reports for the CAMARA project ecosystem. The workflow provides:

- **API Release Analysis** - Track API versions, meta-release categorization, and quality consistency across all CAMARA API repositories
- **Repository Overview Reports** - Monitor repository health, activity patterns, and project statistics organization-wide
- **Quality Assurance** - Identify version mismatches, documentation gaps, and consistency issues
- **Automated Scheduling** - Weekly automated reports with on-demand execution capabilities

## Key Features

✅ **Cross-Repository Analysis** - Analyzes all repositories in the `camaraproject` organization  
✅ **Parallel Processing** - Fast execution (3-5 minutes) using matrix-based parallel analysis  
✅ **Smart Categorization** - Automatic meta-release detection and API classification  
✅ **Flexible Filtering** - Configurable inclusion of pre-releases, legacy releases, and archived repositories  
✅ **Quality Monitoring** - Proactive detection of versioning and documentation issues  

## Getting Started

📖 **[Complete Documentation](documentation/project-admin-generate-reports.md)**

The comprehensive user guide includes:
- Prerequisites and setup instructions
- Step-by-step configuration (including Fine-grained PAT setup)
- Usage scenarios and best practices
- Report interpretation guide
- Troubleshooting and FAQ

## Quick Links

- **[User Documentation](documentation/project-admin-generate-reports.md)** - Complete setup and usage guide
- **[Workflow File](.github/workflows/project-admin-generate-reports.yml)** - The GitHub Actions workflow
- **Actions Tab** - Run reports and view execution history

## Support

For questions, issues, or contributions, please refer to the [troubleshooting section](documentation/project-admin-generate-reports.md#troubleshooting) in the documentation or open an issue in this repository.