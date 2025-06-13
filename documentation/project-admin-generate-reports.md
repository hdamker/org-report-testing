# CAMARA Reporting Workflows - User Documentation

## Table of Contents
1. [Purpose](#purpose)
2. [Prerequisites](#prerequisites)
3. [Quick Start](#quick-start)
4. [Workflow Configuration](#workflow-configuration)
5. [Usage Guide](#usage-guide)
6. [Understanding Reports](#understanding-reports)
7. [Advanced Features](#advanced-features)
8. [Troubleshooting](#troubleshooting)
9. [FAQ](#faq)

---

## Purpose

The CAMARA Reporting Workflows are two specialized automated GitHub Actions workflows that provide comprehensive analysis and reporting for CAMARA project repositories:

### 🏢 **Repository Overview Workflow**
- **Repository Health Monitoring** - Track activity patterns, contribution statistics, and project health metrics
- **Template Compliance Verification** - Ensure API repositories follow CAMARA template standards (6 comprehensive checks)
- **Organization-wide Statistics** - Complete overview of all CAMARA repositories by type
- **Quality Assurance** - Identify documentation gaps and template violations

### 📦 **API Releases Workflow**
- **API Release Tracking** - Monitor release status across all API repositories
- **Recent Release Analysis** - Track releases published in the last 30 days
- **Repository Categorization** - Identify repos with/without releases
- **Future Expansion Ready** - Placeholder for meta-release analysis, API version tracking, and quality checks

### Key Benefits
- ✅ **Specialized Focus** - Each workflow optimized for its specific purpose
- ✅ **Cross-Repository Insights** - Organization-wide visibility across all CAMARA repos
- ✅ **Automated Analysis** - No manual data collection required
- ✅ **Consistent Reporting** - Standardized metrics and formats
- ✅ **Fast Processing** - Optimized performance with batch processing
- ✅ **Quality Monitoring** - Proactive issue detection and template compliance

---

## Prerequisites

### Required Access
- **GitHub Account** with access to run workflows in your repository
- **CAMARA Organization Access** - You must be a member or have read access to `camaraproject` organization
- **Repository Permissions** - Admin or write access to the repository where you'll run the workflows
- **Token Approval** - Fine-grained PAT requires approval from CAMARA organization administrators

### Technical Requirements
- Repository with GitHub Actions enabled
- Both workflow files deployed to `.github/workflows/` directory
- Fine-grained Personal Access Token (FGPAT) configured

### Knowledge Prerequisites
- Basic understanding of GitHub Actions
- Familiarity with Markdown report format
- Understanding of API repository concepts (helpful for interpreting reports)

---

## Quick Start

### 1. Deploy the Workflows
1. Copy both workflow files to `.github/workflows/` in your repository:
   - `camara-repository-overview.yml` - Repository health and template compliance
   - `camara-api-releases.yml` - API release tracking and analysis
2. Commit and push the files to your main branch

### 2. Configure Authentication
1. **Create Fine-grained Personal Access Token**:
   - Go to **GitHub Settings** → **Developer settings** → **Personal access tokens** → **Fine-grained tokens**
   - Click **Generate new token**
   - **Resource owner**: Select `camaraproject` organization
   - **Repository access**: Select **"All repositories"** 
   - **Repository permissions**: Contents (Read), Metadata (Read), Issues (Read), Pull requests (Read), Actions (Read)
   - **Organization permissions**: Members (Read), Administration (Read)
   - **Important**: Token requires approval from CAMARA organization administrators

2. **Add Token as Repository Secret**:
   - **Wait for token approval** from CAMARA administrators (check token status in your GitHub settings)
   - Once approved, copy the token value
   - Go to your repository **Settings** → **Secrets and variables** → **Actions**
   - Click **New repository secret**
   - Name: `CAMARA_TOKEN`
   - Value: Paste your approved token
   - Click **Add secret**

### 3. Run Your First Report
1. Go to **Actions** tab in your repository
2. Select **"CAMARA Repository Overview"** for your first run
3. Click **"Run workflow"**
4. Configure parameters:
   ```
   Include archived: false
   Detailed activity: false
   Template compliance: false
   ```
5. Click **"Run workflow"** to start
6. Download the report from **Artifacts** when complete

---

## Workflow Configuration

### Repository Overview Workflow Parameters

**Include Archived Repositories** (`true`/`false`, default: `false`)
- **Enabled**: Archived repositories included in statistics and listings
- **Disabled**: Only active repositories analyzed

**Detailed Activity Analysis** (`true`/`false`, default: `false`)
- **Enabled**: Deep activity analysis using commits, issues, PRs (slower but more accurate)
- **Disabled**: Fast analysis using repository metadata only

**Template Compliance Checks** (`true`/`false`, default: `false`)
- **Enabled**: Performs comprehensive 6-point template compliance verification for API repositories
- **Disabled**: Skips template compliance analysis (faster processing)

### API Releases Workflow Parameters

**Include Pre-releases** (`true`/`false`, default: `false`)
- **Enabled**: Pre-releases included in analysis and recent releases tracking
- **Disabled**: Pre-releases excluded from main analysis

**Include Legacy Releases** (`true`/`false`, default: `false`)
- **Enabled**: Legacy releases included in analysis
- **Disabled**: Legacy releases excluded from main analysis

### Scheduling

**Repository Overview Workflow**:
- **Automatic**: Weekly on Mondays at 07:35 UTC
- **Manual**: On-demand execution with custom parameters

**API Releases Workflow**:
- **Manual Only**: Triggered on-demand (can be scheduled if needed)

---

## Usage Guide

### Running Repository Overview Reports

#### Method 1: GitHub Web Interface
1. Navigate to **Actions** tab
2. Select **"CAMARA Repository Overview"**
3. Click **"Run workflow"** 
4. Configure parameters based on your needs:

   **Quick Health Check** (Fast):
   ```
   Include archived: false
   Detailed activity: false
   Template compliance: false
   ```

   **Comprehensive Analysis** (Detailed):
   ```
   Include archived: false
   Detailed activity: true
   Template compliance: true
   ```

5. Click **"Run workflow"**

#### Method 2: GitHub CLI
```bash
# Quick health check
gh workflow run "CAMARA Repository Overview" \
  --field include_archived=false \
  --field detailed_activity=false \
  --field template_compliance=false

# Comprehensive analysis
gh workflow run "CAMARA Repository Overview" \
  --field include_archived=false \
  --field detailed_activity=true \
  --field template_compliance=true
```

### Running API Releases Reports

#### Method 1: GitHub Web Interface
1. Navigate to **Actions** tab
2. Select **"CAMARA API Releases"**
3. Click **"Run workflow"**
4. Configure parameters:

   **Standard Release Tracking**:
   ```
   Include prerelease: false
   Include legacy: false
   ```

   **Complete Release Analysis**:
   ```
   Include prerelease: true
   Include legacy: true
   ```

5. Click **"Run workflow"**

#### Method 2: GitHub CLI
```bash
# Standard tracking
gh workflow run "CAMARA API Releases" \
  --field include_prerelease=false \
  --field include_legacy=false

# Complete analysis
gh workflow run "CAMARA API Releases" \
  --field include_prerelease=true \
  --field include_legacy=true
```

### Common Usage Scenarios

**Weekly Project Health Monitoring**:
```
Workflow: Repository Overview
Include archived: false
Detailed activity: false
Template compliance: false
```
*Fast overview for regular monitoring*

**Quarterly Template Compliance Audit**:
```
Workflow: Repository Overview
Include archived: false
Detailed activity: false
Template compliance: true
```
*Focus on template compliance verification*

**Monthly API Release Review**:
```
Workflow: API Releases
Include prerelease: false
Include legacy: false
```
*Track official API releases*

**Pre-Release Development Tracking**:
```
Workflow: API Releases
Include prerelease: true
Include legacy: false
```
*Include development releases for comprehensive tracking*

---

## Understanding Reports

### Repository Overview Report

#### Executive Summary
- Total repositories and breakdown by type (Sandbox, Incubating, Working Group, Other)
- Programming languages used across the organization
- Open issues and pull requests statistics
- Template compliance status (when enabled)

#### Key Sections

**Repository Statistics**:
- General statistics (public/private, languages, issues, PRs)
- Repository type breakdown
- Template compliance summary (when enabled)

**Template Compliance Analysis** (when enabled):
- Compliance rate across API repositories
- List of compliant repositories
- Detailed violations table with specific issues

**Activity Analysis** (when detailed mode enabled):
- Comparison between GitHub's updated_at vs. actual activity
- Repositories with significant activity date differences
- Activity type breakdown (commits, issues, PRs)

**Repository Listings**:
- Top repositories by stars
- Recently active repositories
- Complete repository list by type with health metrics

#### Template Compliance Checks

The Repository Overview workflow performs comprehensive template compliance verification:

**For Sandbox API Repositories:**
1. ✅ README must not contain "family" or "families" terms
2. ✅ Repository description must not contain "family" or "families" terms  
3. ✅ Repository description starts with "Sandbox"
4. ✅ Website points to "https://lf-camaraproject.atlassian.net/"
5. ✅ Line 8 of README contains correct Sandbox badge with proper HTML structure
6. ✅ README contains line starting with "Sandbox API Repository to describe, develop, document, and test"

**For Incubating API Repositories:**
1. ✅ README must not contain "family" or "families" terms
2. ✅ Repository description must not contain "family" or "families" terms  
3. ✅ Repository description starts with "Incubating"
4. ✅ Website points to "https://lf-camaraproject.atlassian.net/"
5. ✅ Line 8 of README contains correct Incubating badge with proper HTML structure
6. ✅ README contains line starting with "Incubating API Repository to evolve and maintain the definitions and documentation"

**Compliance Reporting**:
- Repositories passing all checks receive "Template used ✅" status
- Individual violations listed with specific check type and issue description
- Compliance rate calculated as percentage of passing API repositories

### API Releases Report

#### Executive Summary
- Total API repositories analyzed
- Repositories with releases vs. without releases
- Total releases found across all repositories
- Filter settings applied

#### Key Sections

**API Repository Summary**:
- Complete list of API repositories with release status
- Repository type (Sandbox/Incubating) and descriptions
- Clear indication of which repos have releases

**Recent Releases** (Last 30 Days):
- All releases published in the last month
- Release details including date, type, and pre-release status
- Links to repositories and specific releases

**Repositories Without Releases**:
- API repositories that don't have any releases yet
- Helps identify repos in early development stages

#### Current Limitations & Future Enhancements

**Current Functionality**:
- ✅ Basic release status tracking
- ✅ Recent release identification
- ✅ Repository categorization by release status

**Planned Future Functionality**:
- 🔄 Meta-release categorization (Fall24, Spring25, Fall25)
- 🔄 API definitions extraction and version tracking
- 🔄 Release consistency analysis
- 🔄 API version progression monitoring
- 🔄 Quality checks between main branch and releases
- 🔄 Parallel processing for faster execution

---

## Advanced Features

### Repository Overview Advanced Features

**Enhanced Template Compliance**:
- README content analysis including specific line verification
- Badge HTML structure validation
- Website URL pattern matching
- Comprehensive violation reporting with actionable details

**Activity Analysis Modes**:
- **Simple Mode**: Uses GitHub's repository updated_at timestamp
- **Detailed Mode**: Analyzes actual commits, issues, and PRs for more accurate activity dates
- **Comparison Reporting**: Shows differences between simple and detailed analysis

**Batch Processing**:
- Processes repositories in batches to avoid API timeouts
- Graceful error handling for individual repository failures
- Comprehensive error reporting

### API Releases Advanced Features

**Repository Filtering**:
- Automatic identification of API repositories via topics
- Separation of Sandbox vs. Incubating repositories
- Exclusion of archived repositories

**Release Analysis**:
- Recent release tracking with configurable time windows
- Pre-release vs. public release distinction
- Error handling for repositories with access issues

**Future Expansion Architecture**:
- Modular design ready for meta-release analysis
- Placeholder structure for API definitions extraction
- Framework for parallel processing implementation

---

## Troubleshooting

### Common Issues

#### Workflow Fails to Start
**Symptoms**: Workflow doesn't appear in Actions or fails immediately

**Solutions**:
- ✅ Verify both workflow files are in `.github/workflows/` directory
- ✅ Check YAML syntax using online validators
- ✅ Ensure GitHub Actions are enabled for the repository
- ✅ Verify you have workflow execution permissions

#### Authentication Errors
**Symptoms**: "Resource not accessible by integration" or 403 errors

**Solutions**:
- ✅ Verify `CAMARA_TOKEN` secret is configured
- ✅ Check that your Fine-grained PAT has been **approved** by CAMARA admins
- ✅ Ensure token hasn't expired (check GitHub Settings → Personal access tokens)
- ✅ Verify token has all required permissions for `camaraproject` organization
- ✅ Test token manually:
  ```bash
  curl -H "Authorization: token YOUR_TOKEN" \
    https://api.github.com/orgs/camaraproject/repos
  ```

**Token Approval Process**:
- Token requests with `camaraproject` as resource owner require admin approval
- Check token status in GitHub Settings → Personal access tokens → Fine-grained tokens
- Contact CAMARA admin team if approval is delayed
- Ensure you requested all required permissions when creating the token

#### Performance Issues
**Symptoms**: Workflows run longer than expected or timeout

**Repository Overview Solutions**:
- ✅ Disable "Detailed activity analysis" for faster runs
- ✅ Disable "Template compliance checks" for basic reports
- ✅ Run during off-peak hours to avoid GitHub API congestion

**API Releases Solutions**:
- ✅ Monitor workflow logs for API rate limiting
- ✅ Consider running with fewer filter options initially
- ✅ Check for repositories causing access errors

#### Missing Data in Reports
**Symptoms**: Expected repositories not appearing in reports

**Repository Overview**:
- ✅ Check if repositories are archived (excluded by default)
- ✅ Verify repository topics are set correctly
- ✅ Review processing errors section in report

**API Releases**:
- ✅ Ensure repositories have `sandbox-api-repository` or `incubating-api-repository` topics
- ✅ Check if repositories are archived (automatically excluded)
- ✅ Verify repository accessibility with your token

#### Template Compliance Issues
**Symptoms**: Unexpected compliance violations or missing checks

**Solutions**:
- ✅ Verify README.md exists in repository root
- ✅ Check that line 8 of README contains exact badge HTML
- ✅ Ensure repository description and homepage are set correctly
- ✅ Review violation details in compliance issues table

### Debugging Steps

1. **Check Workflow Logs**:
   - Go to Actions tab → Select failed run → View logs
   - Look for specific error messages and failure points
   - Check which repositories caused processing errors

2. **Verify Token Status**:
   - Go to GitHub Settings → Developer settings → Personal access tokens → Fine-grained tokens
   - Check token status (Active/Pending/Expired)
   - Verify expiration date and permissions

3. **Test API Access Manually**:
   ```bash
   # Test basic organization access
   curl -H "Authorization: token YOUR_TOKEN" \
     https://api.github.com/orgs/camaraproject

   # Test repository listing
   curl -H "Authorization: token YOUR_TOKEN" \
     https://api.github.com/orgs/camaraproject/repos?per_page=5
   ```

4. **Validate Repository Setup**:
   - Check that target repositories have correct topics
   - Verify repository descriptions and homepages are set
   - Ensure README.md files exist and follow expected format

---

## FAQ

### General Questions

**Q: How often should I run these workflows?**
A: Repository Overview weekly (automated), API Releases monthly or as needed for release tracking.

**Q: Can I run these workflows from any repository?**
A: Yes, as long as you have the proper FGPAT configured for cross-organization access to `camaraproject`.

**Q: What's the difference between the two workflows?**
A: Repository Overview focuses on general health and template compliance; API Releases focuses on release tracking and version analysis.

**Q: Which workflow should I run first?**
A: Start with Repository Overview as it provides the foundation understanding of all repositories, then use API Releases for specific release tracking needs.

### Technical Questions

**Q: Why do I need a Fine-grained Personal Access Token?**
A: The default GITHUB_TOKEN only works within the same repository/organization. You need elevated permissions to access the CAMARA organization from your personal repository.

**Q: Do I need admin rights in CAMARA to create the token?**
A: No, you create the token request with `camaraproject` as the resource owner, and the CAMARA admin team will review and approve it.

**Q: How long does token approval take?**
A: This depends on the CAMARA admin team's review process. Contact them directly if you need expedited approval.

**Q: Why can't I use my personal account as the resource owner?**
A: Fine-grained PATs with personal account as resource owner cannot set Organization Permissions for other organizations like `camaraproject`.

**Q: Can I schedule the API Releases workflow?**
A: Yes, you can add a schedule section to the workflow file if you want automated API release tracking.

### Repository Overview Questions

**Q: What does "Template used ✅" mean?**
A: This indicates that an API repository passes all 6 template compliance checks, including proper README format, badges, descriptions, and website links.

**Q: When should I enable template compliance checks?**
A: Enable when you need to audit API repositories for CAMARA template adherence. Disable for faster reports focused on activity and statistics.

**Q: Why is detailed activity analysis slower?**
A: It analyzes actual commits, issues, and PRs instead of just using GitHub's repository updated_at timestamp, requiring additional API calls.

**Q: What's the difference between simple and detailed activity analysis?**
A: Simple uses GitHub's updated_at field; detailed analyzes actual commits, issues, and PRs for more accurate last activity dates.

### API Releases Questions

**Q: Why does the API Releases report show limited information?**
A: The current version provides basic release tracking. Full functionality including meta-release analysis and API version tracking is planned for future implementation.

**Q: What does "Repositories Without Releases" mean?**
A: These are API repositories that have the proper topics but haven't published any releases yet.

**Q: When will the full API Releases functionality be available?**
A: The workflow is designed for easy expansion. Full functionality can be implemented based on specific requirements and priorities.

**Q: Can I modify the API Releases workflow to add more features?**
A: Yes, the workflow is structured to allow easy extension. Contact the workflow maintainer for guidance on specific enhancements.

### Troubleshooting

**Q: The workflow runs but produces empty reports - why?**
A: Usually a permissions issue. Verify your FGPAT has access to the CAMARA organization and all required repository permissions.

**Q: Some repositories are missing from the reports - why?**
A: Check if they have the required topics and aren't archived. Repository Overview includes all repos; API Releases only includes those with API topics.

**Q: What if I see processing errors in the reports?**
A: Processing errors are normal for some repositories due to API rate limits or access restrictions. The workflows continue processing and report which repositories had issues.

**Q: Template compliance shows violations I disagree with - what should I do?**
A: Review the specific violation details in the report. The checks are based on CAMARA template standards - contact the template maintainers if standards need updating.

---

## Support and Contributions

For issues, questions, or contributions:

1. **Check this documentation first** - Most questions are answered here
2. **Review workflow logs** for specific error messages and failure points
3. **Test token permissions manually** using the provided curl commands
4. **Open an issue** in your repository with detailed error information and logs

### Security Reminder
**Never share your personal access token** in issues, pull requests, or public communications. Tokens should be kept secure and rotated regularly.

### Workflow Enhancement Requests
For requests to enhance or extend the workflows (especially API Releases functionality):
- Describe the specific use case and requirements
- Provide examples of desired output or analysis
- Consider the impact on processing time and complexity

---

*This documentation covers both CAMARA Reporting Workflows. For workflow-specific questions, refer to the relevant sections above.*