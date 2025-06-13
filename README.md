# CAMARA Reporting Workflows

## Two Specialized Workflows for CAMARA Project Analysis

This repository contains **two separate GitHub Actions workflows** that provide comprehensive analysis and reporting for the CAMARA project ecosystem:

| Workflow | File | Purpose | Schedule |
|----------|------|---------|----------|
| 🏢 **Repository Overview** | `camara-repository-overview.yml` | Health monitoring & template compliance | Weekly (Mondays 07:35 UTC) |
| 📦 **API Releases** | `camara-api-releases.yml` | Release tracking & analysis | Manual trigger |

---

## 🏢 Repository Overview Workflow

**File**: `.github/workflows/camara-repository-overview.yml`

### What it does:
- **Repository Health Monitoring** - Track activity patterns, contribution statistics, and project health metrics
- **Template Compliance Verification** - Comprehensive 6-point verification that API repositories follow CAMARA template standards
- **Organization-wide Statistics** - Complete overview of all CAMARA repositories by type
- **Quality Assurance** - Identify documentation gaps and template violations

### Key Features:
- ✅ **Fully Functional** - Complete implementation with all features
- ✅ **Template Compliance** - 6 comprehensive checks for API repositories
- ✅ **Activity Analysis** - Simple and detailed modes available
- ✅ **Automated Scheduling** - Runs weekly automatically
- ✅ **Proven Stable** - Thoroughly tested and reliable

---

## 📦 API Releases Workflow

**File**: `.github/workflows/camara-api-releases.yml`

### What it does:
- **API Release Tracking** - Monitor release status across all API repositories
- **Recent Release Analysis** - Track releases published in the last 30 days
- **Repository Categorization** - Identify repos with/without releases
- **Future Expansion Ready** - Framework for comprehensive release analysis

### Current Status:
- ✅ **Basic Functionality** - Release status tracking and recent releases
- 🔄 **Expansion Ready** - Structured for adding meta-release analysis, API version tracking, and quality checks

---

## Why Two Separate Workflows?

| Benefit | Description |
|---------|-------------|
| **🎯 Specialized Focus** | Each workflow optimized for its specific purpose |
| **⚡ Independent Execution** | Run repository health checks separately from release analysis |
| **📅 Flexible Scheduling** | Repository overview runs weekly; releases run on-demand |
| **🔧 Easier Maintenance** | Smaller, focused workflows are easier to maintain and extend |
| **🚀 Better Performance** | Optimized execution without unnecessary complexity |

---

## Quick Start

### 1. Deploy Both Workflow Files

Copy these **two files** to your `.github/workflows/` directory:

```
.github/workflows/
├── camara-repository-overview.yml    ← Repository health & compliance
└── camara-api-releases.yml           ← API release tracking
```

### 2. Configure Authentication

Set up a Fine-grained Personal Access Token as `CAMARA_TOKEN` secret  
📖 [See detailed setup instructions](documentation/project-admin-generate-reports.md#quick-start)

### 3. Run Your First Reports

**Start with Repository Overview:**
1. Go to **Actions** → **"CAMARA Repository Overview"**
2. Click **"Run workflow"** with default settings
3. Download report from **Artifacts**

**Then try API Releases:**
1. Go to **Actions** → **"CAMARA API Releases"**  
2. Click **"Run workflow"** with default settings
3. Download report from **Artifacts**

---

## What Reports Look Like

### 🏢 Repository Overview Report Includes:
- **Repository Statistics** - Type breakdown (Sandbox, Incubating, Working Group, Other)
- **Template Compliance Analysis** - 6-point verification with violation details (when enabled)
- **Activity Analysis** - Recent activity and detailed comparison (when enabled)
- **Top Repositories** - By stars and recent activity
- **Complete Repository Listings** - Organized by type with health metrics

### 📦 API Releases Report Includes:
- **API Repository Summary** - All API repositories with release status
- **Recent Releases** - Releases published in last 30 days
- **Repositories Without Releases** - API repos in early development
- **Future Enhancements** - Roadmap for meta-release analysis and version tracking

---

## Documentation & Links

### 📚 Complete Documentation
- **[User Documentation](documentation/project-admin-generate-reports.md)** - Complete setup and usage guide for both workflows

### ⚙️ Workflow Files
- **[Repository Overview Workflow](.github/workflows/camara-repository-overview.yml)** - Health monitoring & template compliance
- **[API Releases Workflow](.github/workflows/camara-api-releases.yml)** - Release tracking & analysis

### 🎯 Usage
- **Actions Tab** - Run workflows and view execution history
- **Artifacts** - Download generated reports after workflow completion

---

## Current Status & Roadmap

### ✅ Repository Overview - Production Ready
- **Status**: Fully functional with comprehensive features
- **Features**: Template compliance, activity analysis, repository statistics
- **Reliability**: Proven stable with weekly automated runs
- **Maintenance**: Active maintenance and updates

### 🔄 API Releases - Basic + Expansion Framework  
- **Current**: Basic release tracking and recent release analysis
- **Planned**: Meta-release categorization (Fall24, Spring25, Fall25)
- **Roadmap**: API version tracking, quality checks, parallel processing
- **Timeline**: Expandable based on requirements and priorities

---

## Support

### Quick Help
1. **📖 Check Documentation** - [Complete guide](documentation/project-admin-generate-reports.md) covers both workflows
2. **🔍 Review Logs** - Check workflow execution logs for specific errors
3. **🔑 Verify Token** - Ensure FGPAT is approved by CAMARA admins
4. **❓ Open Issue** - Provide workflow name and detailed error information

### Common Questions
- **Which workflow should I use?** - Start with Repository Overview for general health, add API Releases for release tracking
- **Can I run both?** - Yes! They're completely independent and complement each other
- **Do I need special permissions?** - You need a Fine-grained PAT approved by CAMARA organization admins

---

**Ready to start?** 📖 [Follow the complete setup guide](documentation/project-admin-generate-reports.md)