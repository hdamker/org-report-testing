# CAMARA Reporting Workflow - User Documentation

## Table of Contents
1. [Purpose](#purpose)
2. [Prerequisites](#prerequisites)
3. [Quick Start](#quick-start)
4. [Configuration](#configuration)
5. [Usage Guide](#usage-guide)
6. [Understanding Reports](#understanding-reports)
7. [Advanced Features](#advanced-features)
8. [Troubleshooting](#troubleshooting)
9. [FAQ](#faq)

---

## Purpose

The CAMARA Reporting Workflow is an automated GitHub Actions workflow that provides comprehensive analysis and reporting for CAMARA project repositories. It helps project maintainers and stakeholders understand:

- **API Release Status**: Track API versions, meta-release categorization, and release consistency
- **Repository Activity**: Monitor repository health, contribution patterns, and project momentum
- **Quality Assurance**: Identify version mismatches, documentation gaps, and consistency issues
- **Project Overview**: Get bird's-eye view of the entire CAMARA ecosystem

### Key Benefits
- ✅ **Automated Analysis** - No manual data collection required
- ✅ **Cross-Repository Insights** - Organization-wide visibility
- ✅ **Consistent Reporting** - Standardized metrics and formats
- ✅ **Quality Monitoring** - Proactive issue detection
- ✅ **Fast Processing** - Parallel execution for large repository sets

---

## Prerequisites

### Required Access
- **GitHub Account** with access to run workflows in your repository
- **CAMARA Organization Access** - You must be a member or have read access to `camaraproject` organization
- **Repository Permissions** - Admin or write access to the repository where you'll run the workflow
- **Token Approval** - Fine-grained PAT requires approval from CAMARA organization administrators

### Technical Requirements
- Repository with GitHub Actions enabled
- Workflow file deployed to `.github/workflows/` directory
- Fine-grained Personal Access Token (FGPAT) configured

### Knowledge Prerequisites
- Basic understanding of GitHub Actions
- Familiarity with Markdown report format
- Understanding of API versioning concepts (helpful for interpreting reports)

---

## Quick Start

### 1. Deploy the Workflow
1. Copy the workflow file to `.github/workflows/project-admin-generate-reports.yml` in your repository
2. Commit and push the file to your main branch

### 2. Configure Authentication
1. **Create Fine-grained Personal Access Token**:
   - Go to **GitHub Settings** → **Developer settings** → **Personal access tokens** → **Fine-grained tokens**
   - Click **Generate new token**
   - **Resource owner**: Select `camaraproject` organization
   - **Repository access**: Select **"All repositories"** (or choose specific CAMARA repos if preferred)
   - **Repository permissions**:
     - Contents: **Read**
     - Metadata: **Read** 
     - Issues: **Read**
     - Pull requests: **Read**
     - Actions: **Read**
   - **Organization permissions**:
     - Members: **Read**
     - Administration: **Read**
   - **Note**: This token will require approval from CAMARA organization administrators

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
2. Select **"Generate CAMARA Project Reports"**
3. Click **"Run workflow"**
4. Configure parameters:
   ```
   Report type: repository-overview
   Include archived: false
   Detailed activity: false
   Template compliance: false
   ```
5. Click **"Run workflow"** to start
6. Download the report from **Artifacts** when complete

---

## Configuration

### Workflow Parameters

The workflow accepts several input parameters to customize report generation:

#### Report Type
- **`repository-overview`** *(Default)*
  - General repository statistics and activity
  - Good for understanding project health
  - Fast execution (~2-3 minutes)

- **`api-releases`**
  - Detailed API version analysis
  - Meta-release categorization
  - Quality and consistency checks
  - Longer execution (~3-5 minutes with parallel processing)

#### API Releases Report Options

**Include Pre-releases** (`true`/`false`, default: `false`)
- **Enabled**: Pre-releases included in analysis, API counts, and recent activity
- **Disabled**: Pre-releases excluded from main analysis (pre-release-only repos still tracked)

**Include Legacy Releases** (`true`/`false`, default: `false`)
- **Enabled**: Legacy releases (non-rX.Y format) included in all analysis
- **Disabled**: Legacy releases excluded from main analysis

**Detailed Activity Analysis** (`true`/`false`, default: `false`)
- **Enabled**: Deep activity analysis using commits, issues, PRs (15-20 minutes)
- **Disabled**: Fast analysis using repository metadata (3-5 minutes)

#### Repository Overview Options

**Include Archived Repositories** (`true`/`false`, default: `false`)
- **Enabled**: Archived repositories included in statistics
- **Disabled**: Only active repositories analyzed

**Template Compliance Checks** (`true`/`false`, default: `false`)
- **Enabled**: Performs comprehensive template compliance verification for API repositories
- **Disabled**: Skips template compliance analysis (faster processing)

### Scheduling

The workflow can run automatically:
- **Weekly Schedule**: Mondays at 07:35 UTC (for repository-overview reports)
- **Manual Trigger**: On-demand execution with custom parameters

---

## Usage Guide

### Running Reports

#### Method 1: GitHub Web Interface
1. Navigate to **Actions** tab
2. Select **"Generate CAMARA Project Reports"**
3. Click **"Run workflow"** 
4. Configure parameters:
   ```
   Report type: api-releases
   Include archived: false
   Detailed activity: false
   Template compliance: false
   Include prerelease: false
   Include legacy: false
   ```
5. Click **"Run workflow"**

#### Method 2: GitHub CLI
```bash
gh workflow run "Generate CAMARA Project Reports" \
  --field report_type=api-releases \
  --field include_archived=false \
  --field detailed_activity=false \
  --field template_compliance=false \
  --field include_prerelease=false \
  --field include_legacy=false
```

### Common Usage Scenarios

**Standard Production Report** *(Recommended)*:
```
Report Type: api-releases
Include pre-releases: false
Include legacy releases: false
Detailed activity: false
Include archived: false
```
*Shows only official releases, fast processing*

**Complete Historical Analysis**:
```
Report Type: api-releases  
Include pre-releases: true
Include legacy releases: true
Detailed activity: true
Include archived: true
```
*Comprehensive analysis, slower but complete*

**Development Tracking**:
```
Report Type: api-releases
Include pre-releases: true
Include legacy releases: false
Detailed activity: false
Include archived: false
```
*Includes latest pre-releases for development insights*

**Project Health Check**:
```
Report Type: repository-overview
Include archived: false
Detailed activity: true
Template compliance: false
```
*Focus on repository activity and contributor patterns*

**Comprehensive Repository Analysis**:
```
Report Type: repository-overview
Include archived: false
Detailed activity: true
Template compliance: true
```
*Complete repository overview with template compliance verification*

---

## Understanding Reports

### Repository Overview Report

#### Executive Summary
- Total repositories and breakdown by type
- Programming languages used
- Open issues and pull requests
- Activity analysis comparison (if detailed mode enabled)

#### Key Sections
- **Repository Statistics**: Counts, visibility, features enabled
- **Repository Types**: Sandbox APIs, Incubating APIs, Working Groups, Other
- **Top Repositories**: By stars, recent activity
- **Complete Repository List**: Organized by type with detailed metrics

### API Releases Report

#### Executive Summary
- Total API repositories analyzed
- Filter settings applied
- Processing method and performance

#### Meta-Release Analysis
Meta-releases are categorized based on first release timing:
- **Fall24**: APIs first released in August-September 2024
- **Spring25**: APIs first released in February-March 2025  
- **Fall25**: APIs first released in August-September 2025
- **Patch**: Subsequent releases in same major version (rX.Y)
- **Other release**: APIs released outside meta-release windows
- **Legacy**: Releases not following rX.Y format
- **Pre-release**: Pre-release versions

#### Repository Categories
1. **Repositories with Releases**: Full analysis with release history
2. **Repositories with Pre-releases Only**: Special tracking (always shown)
3. **Repositories Without Releases**: APIs found on main branch only

#### Quality Analysis
- **Version Consistency**: Main branch vs. latest release comparisons
- **Documentation Issues**: Missing version information in release notes
- **API Evolution**: Version progression tracking
- **Template Compliance**: Comprehensive verification that repositories follow CAMARA template standards

### Template Compliance Checks

The workflow automatically verifies that API repositories follow CAMARA template standards:

**For Sandbox API Repositories:**
- ✅ README must not contain "family" or "families" terms
- ✅ Repository description must not contain "family" or "families" terms  
- ✅ Repository description starts with "Sandbox"
- ✅ Website points to "https://lf-camaraproject.atlassian.net/"
- ✅ Line 8 of README contains correct Sandbox badge: `<a href="https://github.com/camaraproject/Governance/blob/main/ProjectStructureAndRoles.md" title="Sandbox API Repository"><img src="https://img.shields.io/badge/Sandbox%20API%20Repository-yellow?style=plastic"></a>`
- ✅ README contains line starting with "Sandbox API Repository to describe, develop, document, and test"

**For Incubating API Repositories:**
- ✅ README must not contain "family" or "families" terms
- ✅ Repository description must not contain "family" or "families" terms  
- ✅ Repository description starts with "Incubating"
- ✅ Website points to "https://lf-camaraproject.atlassian.net/"
- ✅ Line 8 of README contains correct Incubating badge: `<a href="https://github.com/camaraproject/Governance/blob/main/ProjectStructureAndRoles.md" title="Incubating API Repository"><img src="https://img.shields.io/badge/Incubating%20API%20Repository-green?style=plastic"></a>`
- ✅ README contains line starting with "Incubating API Repository to evolve and maintain the definitions and documentation"

Repositories passing all checks receive a "Template used ✅" status. Individual violations are listed in the Template Compliance Analysis section.

### Understanding API Counts

**Important Notes**:
- **"Meta-releases"** count = Fall24 + Spring25 + Fall25 only
- **"All releases"** count = Meta-releases + Other releases (never includes Legacy or Pre-releases)
- **Filter Impact**: Counts reflect applied filters
- **Unique APIs**: Same API name counted once per category

---

## Advanced Features

### Parallel Processing

The API releases report uses matrix-based parallel processing:
- **Automatic Load Balancing**: Repositories split into groups of 8
- **Concurrent Execution**: Up to 6 groups processed simultaneously  
- **Performance Optimization**: 3-5 minutes vs. 15-20 minutes sequential
- **Fault Tolerance**: Individual group failures don't stop entire analysis

### Smart Categorization

**Meta-Release Detection**:
- Analyzes release dates to determine meta-release cycles
- Groups related releases (patches) under primary releases
- Handles version format validation (rX.Y pattern)

**Repository Type Classification**:
- **Sandbox**: `sandbox-api-repository` topic
- **Incubating**: `incubating-api-repository` topic  
- **Working Group**: `workinggroup` topic
- **Other**: No recognized classification topics

### Quality Assurance Features

**Consistency Checks**:
- Main branch vs. latest release version comparison
- Release description completeness validation
- API version progression validation

**Error Handling**:
- Graceful degradation for API failures
- Comprehensive error reporting
- Retry logic for transient failures

---

## Troubleshooting

### Common Issues

#### Workflow Fails to Start
**Symptoms**: Workflow doesn't appear in Actions or fails immediately

**Solutions**:
- ✅ Verify workflow file is in `.github/workflows/` directory
- ✅ Check file syntax with YAML validator
- ✅ Ensure GitHub Actions are enabled for the repository
- ✅ Verify you have workflow execution permissions

#### Authentication Errors
**Symptoms**: "Resource not accessible by integration" or 403 errors

**Solutions**:
- ✅ Verify `CAMARA_TOKEN` secret is configured
- ✅ Check that your Fine-grained PAT has been **approved** by CAMARA admins
- ✅ Ensure token hasn't expired
- ✅ Verify token has all required permissions listed above
- ✅ Test token manually:
  ```bash
  curl -H "Authorization: token YOUR_TOKEN" \
    https://api.github.com/orgs/camaraproject/repos
  ```

**Token Approval Issues**:
- If your token request is pending approval, contact the CAMARA admin team
- Check your token status in GitHub Settings → Personal access tokens
- Ensure you requested all required permissions when creating the token

#### Long Processing Times
**Symptoms**: Workflow runs longer than expected

**Solutions**:
- ✅ Disable "Detailed activity analysis" for faster runs
- ✅ Use default parallel processing (avoid detailed mode)
- ✅ Check GitHub Actions runner availability
- ✅ Consider running during off-peak hours

#### Missing Data in Reports
**Symptoms**: Expected repositories or releases not in report

**Solutions**:
- ✅ Verify filter settings match expectations
- ✅ Check if repositories have required topics
- ✅ Ensure releases are properly tagged
- ✅ Review processing errors section in report

#### Rate Limiting Issues
**Symptoms**: API rate limit exceeded errors

**Solutions**:
- ✅ Workflow includes automatic delays and retries
- ✅ Consider using GitHub App instead of PAT for higher limits
- ✅ Run during off-peak hours
- ✅ Spread multiple runs across time

### Debugging Steps

1. **Check Workflow Logs**:
   - Go to Actions tab → Failed run → View logs
   - Look for specific error messages
   - Check which step failed

2. **Verify Token Permissions**:
   - Test API access manually
   - Check organization membership
   - Verify token scope and permissions

3. **Validate Repository Access**:
   - Ensure you can access CAMARA repositories manually
   - Check if organization has restricted token access
   - Verify repository topics are set correctly

4. **Review Filter Logic**:
   - Understand how filters affect output
   - Test with different filter combinations
   - Check if expectation matches filter behavior

---

## FAQ

### General Questions

**Q: How often should I run reports?**
A: Weekly for monitoring, monthly for detailed analysis. The workflow automatically runs weekly repository overviews.

**Q: Can I run this from any repository?**
A: Yes, as long as you have the proper FGPAT configured for cross-organization access.

**Q: What's the difference between the two report types?**
A: Repository overview focuses on general activity and statistics; API releases provides detailed version analysis and quality checks.

### Technical Questions

**Q: Why do I need a Fine-grained Personal Access Token?**
A: The default GITHUB_TOKEN only works within the same repository/organization. You need elevated permissions to access the CAMARA organization from your personal repository.

**Q: Do I need admin rights in CAMARA to create the token?**
A: No, you don't need admin rights. You create the token request with `camaraproject` as the resource owner, and the CAMARA admin team will review and approve it.

**Q: How long does token approval take?**
A: This depends on the CAMARA admin team's review process. Contact them directly if you need expedited approval for urgent reporting needs.

**Q: Why can't I use my personal account as the resource owner?**
A: Fine-grained PATs with personal account as resource owner cannot set Organization Permissions for other organizations like `camaraproject`. You need the organization as the resource owner to access its repositories.

**Q: What if my token expires?**
A: Generate a new token with the same permissions and update the `CAMARA_TOKEN` secret in your repository.

**Q: Can I modify the workflow for other organizations?**
A: Yes, change the `org` variable in the workflow file from 'camaraproject' to your target organization.

### Report Interpretation

**Q: Why are API counts different between sections?**
A: Different sections use different inclusion criteria. "Meta-releases" only includes Fall24/Spring25/Fall25, while "All releases" adds Other releases but never Legacy or Pre-releases.

**Q: What does "Pre-release-only" mean?**
A: Repositories that have releases but only pre-release versions, no public releases yet. These always appear in the report regardless of filter settings.

**Q: How are meta-releases determined?**
A: Based on the first release date in each major version cycle. APIs first released in August/September are categorized as Fall releases, February/March as Spring releases.

**Q: What does "Template used ✅" mean?**
A: This indicates that an API repository follows all CAMARA template standards, including proper README and description format, correct badges, website links, and absence of deprecated "family/families" terminology.

**Q: Why do some repositories show template compliance violations?**
A: The workflow checks API repositories against comprehensive CAMARA template standards. Common violations include using deprecated "family" terminology, incorrect badges on line 8 of README, wrong website URLs, or missing descriptive lines in README files.

**Q: When should I enable template compliance checks?**
A: Enable template compliance when you need to audit API repositories for CAMARA template adherence. This adds processing time as it requires reading README files. Disable for faster reports focused on activity and statistics.

**Q: Why is template compliance disabled by default?**
A: Template compliance checking requires additional API calls to read README files, which increases processing time. It's optional so users can choose between speed (disabled) and comprehensive analysis (enabled).

### Troubleshooting

**Q: The workflow runs but produces empty reports - why?**
A: Usually a permissions issue. Verify your FGPAT has access to the CAMARA organization and required repository permissions.

**Q: Some repositories are missing from the report - why?**
A: Check if they have the required topics (`sandbox-api-repository`, `incubating-api-repository`, or `workinggroup`) and aren't archived (unless you enabled archived inclusion).

**Q: What if I see processing errors in the report?**
A: Processing errors are normal for some repositories due to API rate limits or access restrictions. The workflow continues processing other repositories and reports which ones had issues.

---

## Support and Contributions

For issues, questions, or contributions:
- Check this documentation first
- Review workflow logs for specific error messages  
- Test token permissions manually
- Open an issue in your repository with detailed error information

Remember to **never share your personal access token** in issues or public communications.