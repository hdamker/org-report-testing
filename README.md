# CAMARA Reporting Workflow

## Overview

The CAMARA Reporting Workflow provides automated analysis and reporting for CAMARA project repositories. It generates comprehensive reports on API releases and repository activity.

## How to Run

1. **Navigate to Actions tab** in your GitHub repository
2. **Select "CAMARA Reporting Workflow"** from the workflows list
3. **Click "Run workflow"** button
4. **Configure the parameters** (see below)
5. **Click "Run workflow"** to start

## Input Parameters

### Report Type
- **`api-releases`** - Analyzes API releases, versions, and meta-release categorization
- **`repository-overview`** - Provides general repository activity and statistics

### API Releases Report Options

#### Filtering Options
- **Include pre-releases** (`true`/`false`, default: `false`)
  - When enabled: Pre-releases appear in analysis, API counts, and recent releases
  - When disabled: Pre-releases excluded from main analysis but pre-release-only repos still tracked

- **Include legacy releases** (`true`/`false`, default: `false`)
  - When enabled: Legacy releases included in analysis and consistency checks
  - When disabled: Legacy releases excluded from main analysis

#### Performance Options
- **Detailed activity analysis** (`true`/`false`, default: `false`)
  - When enabled: More thorough analysis but takes longer (15-20 minutes)
  - When disabled: Faster parallel processing (3-5 minutes)

## Report Outputs

### API Releases Report Contains:

1. **Executive Summary**
   - Total repositories analyzed
   - Filter settings applied
   - Processing method used

2. **Meta-Release Analysis**
   - Release categorization (Fall24, Spring25, Fall25, etc.)
   - API counts by meta-release category
   - Combined API statistics

3. **Recent Activity**
   - Releases published in last 30 days
   - Trending repository activity

4. **Repository Categories**
   - **Repositories with Releases** - Full analysis with release history
   - **Repositories with Pre-releases Only** - Special tracking table (always shown)
   - **Repositories Without Releases** - APIs found on main branch only

5. **Quality Analysis**
   - Consistency issues between main branch and releases
   - Version mismatches and missing documentation

6. **Detailed Repository Breakdown**
   - Per-repository release history
   - API evolution tracking
   - Meta-release assignments

### Security Report Contains:
- CodeQL security scan results
- Vulnerability findings by severity
- Remediation recommendations

### Repository Overview Contains:
- Repository activity metrics
- Contributor statistics
- Issue and PR analytics

## Understanding the Filters

### Typical Usage Scenarios

**Standard Production Report** (recommended):
```
Report Type: api-releases
Include pre-releases: false
Include legacy releases: false
Detailed activity: false
```
*Shows only official releases, fast processing*

**Complete Historical Analysis**:
```
Report Type: api-releases  
Include pre-releases: true
Include legacy releases: true
Detailed activity: true
```
*Shows everything, slower but comprehensive*

**Development Preview**:
```
Report Type: api-releases
Include pre-releases: true
Include legacy releases: false  
Detailed activity: false
```
*Includes latest pre-releases for development tracking*

## Key Features

### Parallel Processing
- Matrix-based parallel analysis for faster execution
- Automatic load balancing across repository groups
- Optimized for large repository sets

### Smart Categorization
- Automatic meta-release detection
- API version consistency tracking
- Pre-release vs. public release differentiation

### Quality Assurance
- Version mismatch detection
- Release documentation validation
- Cross-reference consistency checks

## Output Location

Reports are saved as workflow artifacts and can be downloaded from:
- **GitHub Actions** → **Workflow run** → **Artifacts section**
- File format: Markdown (`.md`)
- File naming: `{report-type}-report-{timestamp}.md`

## Troubleshooting

### Common Issues

**Workflow fails to start:**
- Check repository permissions
- Verify workflow file is in `.github/workflows/`

**Long processing times:**
- Disable "Detailed activity analysis" for faster runs
- Check if too many repositories are being processed

**Missing releases in report:**
- Verify filter settings match your needs
- Check if releases are correctly tagged as pre-releases

**API count seems wrong:**
- Note that "All releases" never includes Legacy or Pre-releases
- Check individual category counts for breakdown

## Notes

- **Processing Time**: 3-5 minutes (parallel) vs 15-20 minutes (detailed)
- **Rate Limits**: Workflow respects GitHub API rate limits
- **Scope**: Analyzes only `camaraproject` organization repositories
- **Filters**: Pre-release-only repositories always appear in special table regardless of filter settings