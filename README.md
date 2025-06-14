# CAMARA Reporting Workflows

Two specialized GitHub Actions workflows for comprehensive CAMARA project analysis:

| Workflow | Purpose | Schedule |
|----------|---------|----------|
| 🏢 **Repository Overview** | Health monitoring & template compliance | Weekly (automated) |
| 📦 **API Releases** | Release tracking & meta-release analysis | Manual trigger |

## Features

**Repository Overview:**
- Repository health monitoring and statistics
- Enhanced template compliance verification (9-point checks with website validation)
- Activity analysis and contribution metrics
- Weekly automated reports with enhanced summaries

**API Releases:**
- Parallel processing for fast execution (3-5 minutes)
- Meta-release categorization (Fall24, Spring25, Fall25)
- API version tracking from OpenAPI specifications
- Consistency validation between main branch and releases

## Quick Start

📖 **[Complete Setup Guide](documentation/project-admin-generate-reports.md)**

The documentation covers:
- Prerequisites and authentication setup
- Workflow deployment instructions
- Configuration options and usage scenarios
- Report interpretation and troubleshooting

## Files

- **[Repository Overview Workflow](.github/workflows/project-report-camara-repository-overview.yml)** - Health monitoring & compliance
- **[API Releases Workflow](.github/workflows/project-report-camara-api-releases.yml)** - Release analysis & tracking
- **[User Documentation](documentation/project-admin-generate-reports.md)** - Complete setup and usage guide