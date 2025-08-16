---
description: 'Comprehensive instructions for creating, updating, and managing Jira issues in the Real Estate Investment Platform project with proper authentication, formatting, and workflow integration.'
applyTo: '**/*.ps1'
---

# Jira Issue Management Instructions

## Your Mission

As GitHub Copilot, you are responsible for ensuring all Jira issue creation and management follows standardized procedures for the Real Estate Investment Platform project. Your mission is to maintain consistency, proper authentication, correct formatting, and seamless integration with the development workflow.

## Overview

This document provides standardized instructions for creating and updating Jira issues in the Real Estate Investment Platform project. All issue creation and updates must follow these guidelines to ensure consistency, proper authentication, and correct formatting.

## Prerequisites

### 1. Environment Variables Setup

Before creating or updating any Jira issues, ensure the persistent environment variables are configured:

```powershell
# Run the environment setup script
.\scripts\jira\Set-PersistentJiraEnvironmentVariables.ps1
```

**Required Environment Variables:**

- `JIRA_ADMINUSER_EMAIL`: Admin user email (`kwhittenberger@mac.com`)
- `JIRA_ADMINAPI_TOKEN`: Admin API token (secure, persistent)
- `JIRA_BASE_URL`: Jira instance URL (`https://kwhittenberger.atlassian.net`)
- `JIRA_USER_EMAIL`: Standard user email (`copilotwhittenberger@gmail.com`)
- `JIRA_API_TOKEN`: Standard user API token (optional, for non-admin operations)

### 2. Authentication Requirements

**MANDATORY:** All issue creation and updates MUST use the Jira Admin credentials:

- ✅ **Always use:** `JIRA_ADMINUSER_EMAIL` and `JIRA_ADMINAPI_TOKEN`
- ❌ **Never use:** Regular user tokens for issue creation
- ❌ **Never hardcode:** Credentials in scripts

## Standardized Jira CRUD Operations

**MANDATORY:** Always use the comprehensive CRUD operations suite for all Jira management tasks:

### Primary Scripts (Required)

- **`scripts/jira/New-JiraIssue.ps1`** - Create issues with full parameter support and ADF descriptions
- **`scripts/jira/Get-JiraIssue.ps1`** - Retrieve issues with flexible search methods and output formats  
- **`scripts/jira/Set-JiraIssue.ps1`** - Update issues with field modifications and status transitions
- **`scripts/jira/Add-JiraComment.ps1`** - Add comments to issues with ADF, Plain, or Markdown formatting
- **`scripts/jira/Remove-JiraIssue.ps1`** - Delete issues with confirmations and cascade options

### Authentication & Setup

- **`scripts/jira/Set-PersistentJiraEnvironmentVariables.ps1`** - Configure environment variables
- **`scripts/jira/Test-JiraConnection.ps1`** - Validate API connectivity

### Documentation

- **`scripts/jira/README-CRUD-Operations.md`** - Comprehensive usage documentation

**CRITICAL RULE:** Never create one-off scripts for Jira operations. Always use the standardized CRUD operations suite.

### Example Usage of CRUD Operations

```powershell
# Create a new story with comprehensive parameters
.\scripts\jira\New-JiraIssue.ps1 -Summary "User authentication system" -Description "Implement secure user authentication and authorization" -IssueType "Story" -StoryPoints 8 -Assignee "copilotwhittenberger@gmail.com" -EpicLink "REIP-25"

# Retrieve issue details
.\scripts\jira\Get-JiraIssue.ps1 -IssueKey "REIP-123"

# Update issue status
.\scripts\jira\Set-JiraIssue.ps1 -IssueKey "REIP-123" -Status "In Progress"

# Search for issues
.\scripts\jira\Get-JiraIssue.ps1 -JQL "sprint = 'Sprint 1' AND project = REIP"

# Delete issue with confirmation
.\scripts\jira\Remove-JiraIssue.ps1 -IssueKey "REIP-123" -Confirm

# Add a comment to an existing Jira issue (Plain text)
.\scripts\jira\Add-JiraComment.ps1 -IssueKey "REIP-108" -Comment "Development completed successfully"

# Add a comment with specific formatting
.\scripts\jira\Add-JiraComment.ps1 -IssueKey "REIP-108" -Comment "**Bold text** and *italic text*" -CommentFormat "Markdown"

# Add an internal comment (visible only to team members)
.\scripts\jira\Add-JiraComment.ps1 -IssueKey "REIP-108" -Comment "Internal notes for team" -Visibility "Internal"
```

## Comment Management with Add-JiraComment.ps1

### Comment Formatting Options

The `Add-JiraComment.ps1` script supports multiple formatting options:

**Plain Text (Default):**

```powershell
.\scripts\jira\Add-JiraComment.ps1 -IssueKey "REIP-123" -Comment "Simple text comment"
```

**Markdown Formatting:**

```powershell
.\scripts\jira\Add-JiraComment.ps1 -IssueKey "REIP-123" -Comment "**Bold** and *italic* text with [links](https://example.com)" -CommentFormat "Markdown"
```

**ADF (Atlassian Document Format):**

```powershell
.\scripts\jira\Add-JiraComment.ps1 -IssueKey "REIP-123" -Comment "Complex formatting" -CommentFormat "ADF"
```

### Comment Visibility Options

**Public Comments (Default):**

```powershell
.\scripts\jira\Add-JiraComment.ps1 -IssueKey "REIP-123" -Comment "Public comment visible to all"
```

**Internal Comments:**

```powershell
.\scripts\jira\Add-JiraComment.ps1 -IssueKey "REIP-123" -Comment "Internal team comment" -Visibility "Internal"
```

**Group-Restricted Comments:**

```powershell
.\scripts\jira\Add-JiraComment.ps1 -IssueKey "REIP-123" -Comment "Developer team only" -Visibility "Internal" -VisibilityGroup "developers"
```

### Common Comment Use Cases

**Development Workflow Completion:**

```powershell
.\scripts\jira\Add-JiraComment.ps1 -IssueKey "REIP-108" -Comment "Development workflow completed successfully. PR #36 merged with commit ce3b9423479f7ab4e42cf43f88e13bd123ca0338. All tests passing (314 total, 313 passed, 1 skipped)."
```

**Status Updates:**

```powershell
.\scripts\jira\Add-JiraComment.ps1 -IssueKey "REIP-123" -Comment "Code review completed. Waiting for final approval before merge."
```

**Technical Documentation:**

```powershell
.\scripts\jira\Add-JiraComment.ps1 -IssueKey "REIP-123" -Comment "**Implementation Notes:**\n- Used Factory pattern for entity creation\n- Added comprehensive validation\n- EF Core configurations applied" -CommentFormat "Markdown"
```

**Issue Resolution:**

```powershell
.\scripts\jira\Add-JiraComment.ps1 -IssueKey "REIP-123" -Comment "Issue resolved. Root cause was RFC 7807 Problem Details implementation changing controller return types. Updated test expectations accordingly."
```

## Legacy Script Management

All legacy and one-off scripts have been moved to `scripts/jira/archive/obsolete-scripts/` directory. These scripts should NOT be used for new development and are preserved only for historical reference.

### Obsolete Scripts (Do Not Use)

Scripts in the archive include but are not limited to:

- Create-*.ps1 (various one-off creation scripts)
- Update-*.ps1 (specific update scripts)  
- Check-*.ps1 (validation scripts now covered by Get-JiraIssue.ps1)
- Verify-*.ps1 (verification scripts now covered by Get-JiraIssue.ps1)
- Assign-*.ps1 (assignment scripts now covered by Set-JiraIssue.ps1)

## Standard Script Format (Deprecated - Use CRUD Operations Instead)

### 1. Script Header Pattern

```powershell
# [Feature Name] - [Operation Description]
# This script [describes what it does] using direct JSON to avoid PowerShell hashtable conversion issues

# Get environment variables for Jira API
$jiraEmail = [Environment]::GetEnvironmentVariable("JIRA_ADMINUSER_EMAIL", "User")
$jiraApiToken = [Environment]::GetEnvironmentVariable("JIRA_ADMINAPI_TOKEN", "User")
$jiraBaseUrl = [Environment]::GetEnvironmentVariable("JIRA_BASE_URL", "User")

if (-not $jiraBaseUrl -or -not $jiraEmail -or -not $jiraApiToken) {
    Write-Error "Missing required environment variables."
    exit 1
}

Write-Host "🚀 [Operation Description]" -ForegroundColor Green
Write-Host "📧 Using credentials for: $jiraEmail" -ForegroundColor Gray
Write-Host "🌐 Base URL: $jiraBaseUrl" -ForegroundColor Gray
```

### 2. HTTP Headers Pattern

```powershell
$headers = @{
    'Authorization' = "Basic $([System.Convert]::ToBase64String([System.Text.Encoding]::ASCII.GetBytes("$jiraEmail`:$jiraApiToken")))"
    'Content-Type' = 'application/json'
    'Accept' = 'application/json'
}
```

### 3. Issue Creation Function

```powershell
# Function to create issue with direct JSON
function Create-Issue {
    param(
        [string]$IssueKey,
        [string]$Summary,
        [string]$JsonBody,
        [int]$StoryPoints
    )
    
    try {
        Write-Host "Creating issue: $IssueKey - $Summary" -ForegroundColor Cyan
        
        $response = Invoke-RestMethod -Uri "$jiraBaseUrl/rest/api/3/issue" -Method Post -Body $JsonBody -Headers $headers
        
        if ($response.key) {
            Write-Host "✅ Created: $($response.key)" -ForegroundColor Green
            
            # Try to set story points
            try {
                $storyPointsJson = @"
{
    "fields": {
        "customfield_10016": $StoryPoints
    }
}
"@
                Invoke-RestMethod -Uri "$jiraBaseUrl/rest/api/3/issue/$($response.key)" -Method Put -Body $storyPointsJson -Headers $headers
                Write-Host "📊 Set story points: $StoryPoints" -ForegroundColor Gray
            } catch {
                Write-Warning "Could not set story points for $($response.key): $($_.Exception.Message)"
            }
            
            $script:createdIssues += @{
                key = $response.key
                summary = $Summary
                storyPoints = $StoryPoints
            }
        }
        
        Start-Sleep -Milliseconds 500  # Rate limiting
        
    } catch {
        Write-Host "❌ Failed: $IssueKey - $($_.Exception.Message)" -ForegroundColor Red
        if ($_.ErrorDetails.Message) {
            Write-Host "Error Details: $($_.ErrorDetails.Message)" -ForegroundColor Red
        }
        $script:failedIssues += @{
            key = $IssueKey
            summary = $Summary
        }
    }
}
```

## Issue JSON Format Standards

### 1. Mandatory Fields

All Jira issues MUST include these fields:

```json
{
  "fields": {
    "project": {"key": "REIP"},
    "summary": "[Clear, descriptive summary]",
    "description": { /* ADF format - see below */ },
    "issuetype": {"name": "Story"},
    "assignee": {"emailAddress": "copilotwhittenberger@gmail.com"},
    "priority": {"name": "High|Medium|Low"},
    "labels": ["relevant", "labels", "here"]
  }
}
```

### 2. ADF (Atlassian Document Format) Description

**MANDATORY:** All issue descriptions MUST use ADF format with the following structure:

```json
"description": {
  "type": "doc",
  "version": 1,
  "content": [
    {
      "type": "panel",
      "attrs": {"panelType": "info"},
      "content": [
        {
          "type": "paragraph",
          "content": [
            {"type": "text", "text": "As a", "marks": [{"type": "strong"}]},
            {"type": "text", "text": " [user type]"},
            {"type": "hardBreak"},
            {"type": "text", "text": "I want", "marks": [{"type": "strong"}]},
            {"type": "text", "text": " [functionality]"},
            {"type": "hardBreak"},
            {"type": "text", "text": "So that", "marks": [{"type": "strong"}]},
            {"type": "text", "text": " [business value]"}
          ]
        }
      ]
    },
    {
      "type": "heading",
      "attrs": {"level": 3},
      "content": [{"type": "text", "text": "Acceptance Criteria"}]
    },
    {
      "type": "bulletList",
      "content": [
        {
          "type": "listItem",
          "content": [
            {
              "type": "paragraph",
              "content": [{"type": "text", "text": "Criterion 1"}]
            }
          ]
        }
      ]
    },
    {
      "type": "heading",
      "attrs": {"level": 3},
      "content": [{"type": "text", "text": "Technical Implementation"}]
    },
    {
      "type": "bulletList",
      "content": [
        {
          "type": "listItem",
          "content": [
            {
              "type": "paragraph",
              "content": [{"type": "text", "text": "Implementation detail 1"}]
            }
          ]
        }
      ]
    },
    {
      "type": "heading",
      "attrs": {"level": 3},
      "content": [{"type": "text", "text": "Business Value"}]
    },
    {
      "type": "paragraph",
      "content": [{"type": "text", "text": "Clear statement of business value"}]
    }
  ]
}
```

### 3. Required Section Structure

Every issue description MUST contain:

1. **User Story Panel** (info panel with As a/I want/So that format)
2. **Acceptance Criteria** (H3 heading with bullet list)
3. **Technical Implementation** (H3 heading with bullet list)
4. **Business Value** (H3 heading with paragraph)

### 4. Assignment Rules

**Default Assignment:**

- All new issues: `copilotwhittenberger@gmail.com`
- Created by: Admin user (`kwhittenberger@mac.com`)

**Epic Assignment:**

- Assign to appropriate Epic after creation
- Use Epic linking for feature grouping

**Auto-Unassignment Policy:**

- **Automatic Behavior**: Moving any issue to "Done" status automatically unassigns it using Set-JiraIssue.ps1
- **Override Capability**: Explicitly specify `-Assignee` parameter to maintain assignment when moving to Done
- **Workflow Integration**: Supports clean task completion and team focus on active work items
- **Implementation**: Built into Set-JiraIssue.ps1 script with automatic detection of Done status transitions

## Critical Rules

### ❌ What NOT to Do

1. **Never use PowerShell hashtables for complex ADF:**

   ```powershell
   # BAD - PowerShell hashtable conversion fails
   $description = @{
       type = "doc"
       content = @{ ... }
   }
   ```

2. **Never hardcode credentials:**

   ```powershell
   # BAD - Security violation
   $jiraEmail = "user@example.com"
   $jiraToken = "hardcoded-token"
   ```

3. **Never skip environment variable validation:**

   ```powershell
   # BAD - No validation
   $jiraEmail = $env:JIRA_ADMINUSER_EMAIL
   ```

4. **Never use regular user tokens for issue creation:**

   ```powershell
   # BAD - Use admin token instead
   $jiraToken = [Environment]::GetEnvironmentVariable("JIRA_API_TOKEN", "User")
   ```

### ✅ What TO Do

1. **Always use direct JSON strings:**

   ```powershell
   # GOOD - Direct JSON avoids conversion issues
   $issueJson = @"
   {
     "fields": {
       "project": {"key": "REIP"},
       ...
     }
   }
   "@
   ```

2. **Always validate environment variables:**

   ```powershell
   # GOOD - Proper validation
   if (-not $jiraBaseUrl -or -not $jiraEmail -or -not $jiraApiToken) {
       Write-Error "Missing required environment variables."
       exit 1
   }
   ```

3. **Always use admin credentials:**

   ```powershell
   # GOOD - Admin credentials for issue creation
   $jiraEmail = [Environment]::GetEnvironmentVariable("JIRA_ADMINUSER_EMAIL", "User")
   $jiraApiToken = [Environment]::GetEnvironmentVariable("JIRA_ADMINAPI_TOKEN", "User")
   ```

4. **Always include rate limiting:**

   ```powershell
   # GOOD - Prevent API throttling
   Start-Sleep -Milliseconds 500
   ```

## Comment Management Best Practices

### When to Add Comments

1. **Development Milestones:**
   - PR merge completion
   - Feature implementation completion  
   - Testing completion
   - Deployment success/failure

2. **Status Updates:**
   - Work progress updates
   - Blocked status with reasons
   - External dependency waiting
   - Review completion

3. **Technical Documentation:**
   - Implementation approach decisions
   - Architecture changes made
   - Performance optimizations applied
   - Bug fix root cause analysis

4. **Communication:**
   - Handoff between team members
   - Clarification requests
   - Stakeholder updates
   - Process deviation explanations

### Comment Formatting Guidelines

**Use Markdown for Rich Content:**

```powershell
# For structured information with formatting
$comment = @"
**Development Completed Successfully**

**Changes Made:**
- Enhanced Address value object with geolocation
- Added new PropertyData entities
- Implemented comprehensive EF Core configurations

**Test Results:**
- Total Tests: 314 (313 passed, 1 skipped)
- Build Status: ✅ Success
- Coverage: Maintained high coverage

**Next Steps:**
1. Database migration generation
2. County assessor integration
3. Analysis engine development
"@

.\scripts\jira\Add-JiraComment.ps1 -IssueKey "REIP-108" -Comment $comment -CommentFormat "Markdown"
```

**Use Plain Text for Simple Updates:**

```powershell
# For quick status updates
.\scripts\jira\Add-JiraComment.ps1 -IssueKey "REIP-108" -Comment "Code review completed. Ready for merge."
```

### Comment Security Considerations

**Public Comments (Default):**

- Visible to all users with access to the issue
- Use for general development updates
- Avoid sensitive technical details

**Internal Comments:**

- Visible only to team members
- Use for internal technical discussions
- Include sensitive implementation details

**Never Include in Comments:**

- API keys or passwords
- Database connection strings
- Personal information

## Script Execution Pattern

### 1. Tracking Variables

```powershell
$createdIssues = @()
$failedIssues = @()
```

### 2. Issue Processing

```powershell
Create-Issue -IssueKey "REIP-XXX-001" -Summary "Issue summary" -JsonBody $issueJson -StoryPoints 8
```

### 3. Summary Report

```powershell
# Display final summary
Write-Host "`n=================================================" -ForegroundColor Green
Write-Host "[Feature] Issue Creation Complete" -ForegroundColor Green
Write-Host "=================================================" -ForegroundColor Green

Write-Host "`n📊 SUMMARY:" -ForegroundColor White
Write-Host "✅ Successfully Created: $($createdIssues.Count) issues" -ForegroundColor Green
Write-Host "❌ Failed: $($failedIssues.Count) issues" -ForegroundColor Red

if ($createdIssues.Count -gt 0) {
    Write-Host "`n📋 CREATED ISSUES:" -ForegroundColor White
    $totalPoints = 0
    foreach ($created in $createdIssues) {
        Write-Host "   $($created.key): $($created.summary) ($($created.storyPoints) points)" -ForegroundColor Cyan
        $totalPoints += $created.storyPoints
    }
    Write-Host "   TOTAL STORY POINTS: $totalPoints" -ForegroundColor Yellow
}

if ($failedIssues.Count -gt 0) {
    Write-Host "`n❌ FAILED ISSUES:" -ForegroundColor Red
    foreach ($failed in $failedIssues) {
        Write-Host "   $($failed.key): $($failed.summary)" -ForegroundColor Red
    }
}
```

## Example Complete Issue JSON

```json
{
  "fields": {
    "project": {"key": "REIP"},
    "summary": "Real-time county assessor data integration",
    "description": {
      "type": "doc",
      "version": 1,
      "content": [
        {
          "type": "panel",
          "attrs": {"panelType": "info"},
          "content": [
            {
              "type": "paragraph",
              "content": [
                {"type": "text", "text": "As a", "marks": [{"type": "strong"}]},
                {"type": "text", "text": " property investor"},
                {"type": "hardBreak"},
                {"type": "text", "text": "I want", "marks": [{"type": "strong"}]},
                {"type": "text", "text": " to access real-time property data from county assessor offices"},
                {"type": "hardBreak"},
                {"type": "text", "text": "So that", "marks": [{"type": "strong"}]},
                {"type": "text", "text": " I can make informed investment decisions with current information"}
              ]
            }
          ]
        },
        {
          "type": "heading",
          "attrs": {"level": 3},
          "content": [{"type": "text", "text": "Acceptance Criteria"}]
        },
        {
          "type": "bulletList",
          "content": [
            {
              "type": "listItem",
              "content": [
                {
                  "type": "paragraph",
                  "content": [{"type": "text", "text": "System can connect to county assessor APIs"}]
                }
              ]
            },
            {
              "type": "listItem",
              "content": [
                {
                  "type": "paragraph",
                  "content": [{"type": "text", "text": "Real-time data retrieval within 30 seconds"}]
                }
              ]
            }
          ]
        },
        {
          "type": "heading",
          "attrs": {"level": 3},
          "content": [{"type": "text", "text": "Technical Implementation"}]
        },
        {
          "type": "bulletList",
          "content": [
            {
              "type": "listItem",
              "content": [
                {
                  "type": "paragraph",
                  "content": [{"type": "text", "text": "Implement IPropertyDataProvider interface"}]
                }
              ]
            },
            {
              "type": "listItem",
              "content": [
                {
                  "type": "paragraph",
                  "content": [{"type": "text", "text": "Create county-specific adapter classes"}]
                }
              ]
            }
          ]
        },
        {
          "type": "heading",
          "attrs": {"level": 3},
          "content": [{"type": "text", "text": "Business Value"}]
        },
        {
          "type": "paragraph",
          "content": [{"type": "text", "text": "Provides competitive advantage through access to current property data from official sources."}]
        }
      ]
    },
    "issuetype": {"name": "Story"},
    "assignee": {"emailAddress": "copilotwhittenberger@gmail.com"},
    "priority": {"name": "High"},
    "labels": ["county-assessor", "data-integration", "mvp"]
  }
}
```

## Troubleshooting

### Common Issues

1. **400 Bad Request - ADF Format Error**
   - **Cause:** PowerShell hashtable conversion to JSON
   - **Solution:** Use direct JSON strings only

2. **401 Unauthorized**
   - **Cause:** Missing or incorrect admin credentials
   - **Solution:** Run environment setup script

3. **Rate Limiting (429)**
   - **Cause:** Too many rapid API calls
   - **Solution:** Ensure `Start-Sleep -Milliseconds 500` between calls

4. **Story Points Not Set**
   - **Cause:** Custom field ID incorrect
   - **Solution:** Verify `customfield_10016` is correct for your instance

### Validation Checklist

Before running any Jira script:

- [ ] Environment variables are set (`JIRA_ADMINUSER_EMAIL`, `JIRA_ADMINAPI_TOKEN`, `JIRA_BASE_URL`)
- [ ] Script uses admin credentials (not regular user)
- [ ] JSON format uses direct strings (not PowerShell hashtables)
- [ ] ADF structure includes all required sections
- [ ] Issues assigned to `copilotwhittenberger@gmail.com`
- [ ] Rate limiting implemented between API calls
- [ ] Error handling and reporting included
- [ ] Summary report displays created issues and story points

## File Locations

- **Environment Setup**: `scripts/jira/Set-PersistentJiraEnvironmentVariables.ps1`
- **Example Scripts**: `scripts/jira/Create-Remaining-Issues.ps1`
- **Documentation**: `docs/development/jira-issue-management.md`

## Integration with Development Workflow

All Jira issue creation must align with the [Development Workflow](../development-workflow.instructions.md):

1. **Task Workflow Tracking**: Use manage_todo_list tool to track all Jira-related activities and progress
2. **Feature Branch Creation**: Use issue keys in branch names
3. **Pull Request Linking**: Reference Jira issues in PR descriptions
4. **Epic Assignment**: Group related issues under appropriate epics
5. **Sprint Planning**: Assign issues to sprints based on priority and capacity

### Todo List Integration for Jira Operations

**MANDATORY: Use manage_todo_list tool for all Jira workflow tasks:**

- **Issue Creation Phase**: Create todos for each issue to be created, mark in-progress before script execution, mark completed after successful creation
- **Issue Management Phase**: Track status updates, field modifications, and comment additions as separate todo items
- **Workflow Integration**: Include Jira operations as part of larger development workflow todo lists
- **Progress Visibility**: Ensure all Jira activities are visible in todo list for stakeholder tracking

---

**Remember:** Consistency in issue creation and management is crucial for project tracking and team collaboration. Always follow these standards when creating or updating Jira issues.
