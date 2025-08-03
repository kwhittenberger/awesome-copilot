---
applyTo: "**"
---

# Development Workflow Instructions

## Overview

This document outlines the mandatory development workflow that **MUST** be followed for all development tasks in the Real Estate Investment Platform project. Following this workflow ensures code quality, proper review processes, and maintains project integrity.

## Core Principles

- **No Direct Commits to Main**: All development work must be done on feature branches
- **Pull Request Required**: All code changes must go through the PR review process
- **Jira Integration**: All work items must be properly tracked and updated in Jira
- **Quality Gates**: All builds, tests, and validations must pass before merge
- **Jira Integration**: All Jira issues MUST have descriptions formatted as AFD

---

## Standard Development Workflow

### Phase 1: Issue Assignment & Planning

#### 1.1 Jira Issue Management

```bash
# ✅ REQUIRED: Assign issue to yourself
# ✅ REQUIRED: Move issue from "Backlog" to "In Development"
# ✅ REQUIRED: Verify Epic assignment and sprint assignment
```

**Validation Checklist:**

- [ ] Issue assigned to developer
- [ ] Status moved to "In Development"
- [ ] Epic and Sprint properly assigned
- [ ] Story points and due date confirmed

#### 1.2 Development Planning

- [ ] Review acceptance criteria and requirements
- [ ] Identify dependencies and prerequisites
- [ ] Plan implementation approach
- [ ] Estimate development time

### Phase 2: Feature Branch Creation

#### 2.1 Branch Naming Convention

```bash
# Feature branches: feature/reip-{issue-number}-{short-description}
# Examples:
feature/reip-41-oauth-provider-config
feature/reip-25-property-analysis-engine
feature/reip-33-user-authentication
```

#### 2.2 Branch Creation Process

```bash
# ✅ REQUIRED: Start from latest main branch
git checkout main
git pull origin main

# ✅ REQUIRED: Create feature branch
git checkout -b feature/reip-{issue-number}-{description}

# ✅ REQUIRED: Push feature branch to origin
git push -u origin feature/reip-{issue-number}-{description}
```

**Validation Checklist:**

- [ ] Feature branch created from latest main
- [ ] Branch follows naming convention
- [ ] Branch pushed to GitHub
- [ ] Local development environment verified

### Phase 3: Implementation

#### 3.1 Development Standards

- [ ] Follow Clean Architecture patterns
- [ ] Implement comprehensive error handling
- [ ] Add appropriate logging and monitoring
- [ ] Write unit tests for new functionality
- [ ] Follow security best practices (OWASP guidelines)
- [ ] Document complex business logic

#### 3.2 Commit Standards

```bash
# ✅ REQUIRED: Use Conventional Commits format
# Examples:
git commit -m "feat(REIP-41): add OAuth provider configuration service"
git commit -m "fix(REIP-25): resolve property analysis calculation bug"
git commit -m "docs(REIP-33): update authentication API documentation"
```

**Commit Message Format:**

```text
<type>(REIP-<number>): <description>

[optional body]

[optional footer]
```

**Types:** `feat`, `fix`, `docs`, `style`, `refactor`, `test`, `chore`

#### 3.3 Development Validation

```bash
# ✅ REQUIRED: Build verification
dotnet build

# ✅ REQUIRED: Test execution
dotnet test

# ✅ REQUIRED: Code quality checks
# Run linting, static analysis, security scans
```

**Validation Checklist:**

- [ ] All builds pass successfully
- [ ] All tests pass
- [ ] No security vulnerabilities introduced
- [ ] Code follows project conventions
- [ ] Documentation updated if needed

### Phase 4: Pull Request Creation

#### 4.1 Pre-PR Checklist

- [ ] All changes committed and pushed
- [ ] Feature branch up to date with main
- [ ] Build passes successfully
- [ ] Tests pass
- [ ] Documentation updated

#### 4.2 PR Creation Process

```bash
# ✅ REQUIRED: Push latest changes
git push origin feature/reip-{issue-number}-{description}

# ✅ REQUIRED: Create PR using GitHub CLI with auto-merge enabled
gh pr create \
  --title "feat(REIP-{number}): {Implementation Title}" \
  --body-file pr-template.md \
  --assignee @me \
  --label "enhancement" \
  --milestone "Sprint 1"

# ✅ OPTIONAL: Enable auto-merge (requires branch protection rules)
gh pr merge --auto --squash
```

#### 4.2.1 Auto-Merge Configuration

**Prerequisites for Auto-Merge:**

- Branch protection rules configured on main branch
- Required status checks enabled (build, tests, security)
- Required reviewers configured (minimum 1)
- Dismiss stale reviews enabled

**Enable Auto-Merge:**

```bash
# Enable auto-merge for current PR
gh pr merge --auto --squash

# Check auto-merge status
gh pr view --json autoMergeRequest
```

#### 4.3 PR Description Template

```markdown
## REIP-{number}: {Title}

### Overview
Brief description of what this PR implements.

### Changes Made
- Key change 1
- Key change 2
- Key change 3

### API Changes (if applicable)
- New endpoints
- Modified endpoints
- Breaking changes

### Testing
- [ ] Unit tests added/updated
- [ ] Integration tests pass
- [ ] Manual testing completed

### Quality Assurance
- [ ] Build passes
- [ ] Tests pass
- [ ] Security scan clean
- [ ] Documentation updated

**Epic**: REIP-{epic-number}
**Sprint**: Sprint {number}
**Story Points**: {points}
**Due Date**: {date}

**Auto-Close Configuration:**
- Closes #{issue-number} (GitHub issue auto-closure)
- Resolves REIP-{number} (Jira integration via webhooks)

**Merge Configuration:**
- Auto-merge: Enabled when all checks pass
- Merge method: Squash and merge
- Delete branch: Automatic after merge
```

### Phase 5: Code Review Process

#### 5.1 Review Requirements

- [ ] **Minimum 1 reviewer** required for approval
- [ ] **Build must pass** before merge
- [ ] **All tests must pass** before merge
- [ ] **Security checks** must pass
- [ ] **No merge conflicts** with main branch

#### 5.2 Review Checklist for Reviewers

**Code Quality:**

- [ ] Code follows Clean Architecture patterns
- [ ] Proper error handling implemented
- [ ] Security best practices followed
- [ ] Performance considerations addressed
- [ ] Code is readable and maintainable

**Testing:**

- [ ] Adequate test coverage
- [ ] Tests are meaningful and robust
- [ ] Edge cases covered
- [ ] Integration points tested

**Documentation:**

- [ ] Public APIs documented
- [ ] Complex logic commented
- [ ] README updates if needed
- [ ] Architecture decisions recorded

### Phase 6: Merge & Deployment

#### 6.1 Automated Merge Process

**Auto-Merge Flow (Recommended):**

```bash
# ✅ Auto-merge handles everything when conditions are met:
# - All required checks pass (build, tests, security)
# - Required approvals received
# - No merge conflicts
# - Branch is up-to-date with main

# Manual verification (optional)
gh pr checks
gh pr view --json mergeable,mergeStateStatus
```

**Manual Merge Process (Fallback):**

```bash
# ✅ REQUIRED: Use "Squash and merge" for feature branches
# ✅ REQUIRED: Delete feature branch after merge
# ✅ REQUIRED: Update local main branch
git checkout main
git pull origin main
git branch -d feature/reip-{issue-number}-{description}
```

#### 6.2 Automated Post-Merge Actions

**GitHub Actions Automation (Triggered on Merge):**

- [ ] **Branch cleanup** - Automatic feature branch deletion
- [ ] **GitHub issue closure** - Via `Closes #` syntax in PR description
- [ ] **Deployment trigger** - Staging environment deployment
- [ ] **Jira status update** - Via webhook integration
- [ ] **Notification dispatch** - Team notifications via Slack/Teams

**Manual Post-Merge Actions (If Automation Fails):**

- [ ] **Verify Jira status** updated to "Done"
- [ ] **Add completion comment** in Jira with PR link
- [ ] **Verify deployment** to staging environment
- [ ] **Update project documentation** if needed
- [ ] **Notify stakeholders** if required

### Phase 7: Automated Issue Management

#### 7.1 GitHub-Jira Integration

**Automated Status Transitions:**

```text
GitHub PR Created → Jira: "In Review"
GitHub PR Approved → Jira: "Ready for Merge"  
GitHub PR Merged → Jira: "Done"
GitHub Issue Closed → Jira: "Resolved"
```

**Webhook Configuration:**

```json
{
  "webhook_url": "https://automation.atlassian.com/pro/hooks/{webhook-id}",
  "events": [
    "pull_request.opened",
    "pull_request.closed",
    "pull_request.merged",
    "issues.closed"
  ],
  "jira_mapping": {
    "pr_opened": "In Review",
    "pr_merged": "Done",
    "issue_closed": "Resolved"
  }
}
```

#### 7.2 Manual Jira Update (Fallback)

**Status Transitions:**

```text
Backlog → In Development → In Review → Done
```

**Jira Update Script Template:**

```powershell
# Update REIP-{number} status to Done after PR merge
$issueKey = "REIP-{number}"
$prUrl = "https://github.com/kwhittenberger/real-estate-requirements/pull/{pr-number}"

# Add completion comment with PR link
# Move status to Done
# Update resolution field
```

---

## Emergency Workflow (Hotfixes)

### Hotfix Branch Process

```bash
# For critical production issues only
git checkout main
git pull origin main
git checkout -b hotfix/reip-{number}-{critical-fix}

# Follow same process but with expedited review
# Requires immediate reviewer approval
# Deploy directly after merge
```

---

## Workflow Violations & Consequences

### ❌ NEVER DO THESE

- **Direct commits to main branch**
- **Merge without PR review**
- **Skip build/test validation**  
- **Bypass Jira status updates**
- **Work on unassigned issues**

### Violation Handling

1. **Immediate rollback** if changes affect main branch
2. **Create proper feature branch** for the work
3. **Follow full workflow process** for correction
4. **Document lesson learned** in project retrospective

---

## Tools & Automation

### Required Tools

- **Git**: Version control
- **GitHub CLI**: PR management and auto-merge
- **PowerShell**: Jira automation scripts
- **dotnet CLI**: Build and test execution

### Automation Scripts

- `scripts/jira/Start-Development-Workflow.ps1` - Initialize workflow
- `scripts/jira/Update-Issue-Status.ps1` - Update Jira status
- `scripts/git/Create-Feature-Branch.ps1` - Create feature branch
- `scripts/validation/Pre-PR-Check.ps1` - Pre-PR validation
- `scripts/automation/Setup-Auto-Merge.ps1` - Configure auto-merge
- `scripts/automation/Verify-Webhook-Integration.ps1` - Test Jira webhooks

### GitHub Actions (Automated)

**Continuous Integration (`ci.yml`):**

```yaml
name: CI
on:
  pull_request:
    branches: [main]
jobs:
  build-and-test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - name: Setup .NET
        uses: actions/setup-dotnet@v4
        with:
          dotnet-version: '9.0.x'
      - name: Build
        run: dotnet build
      - name: Test
        run: dotnet test
      - name: Security Scan
        run: dotnet list package --vulnerable
```

**Auto-Merge Workflow (`auto-merge.yml`):**

```yaml
name: Auto-Merge
on:
  pull_request_review:
    types: [submitted]
jobs:
  auto-merge:
    if: github.event.review.state == 'approved'
    runs-on: ubuntu-latest
    steps:
      - name: Enable auto-merge
        run: gh pr merge --auto --squash ${{ github.event.pull_request.number }}
        env:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
```

**Post-Merge Actions (`post-merge.yml`):**

```yaml
name: Post-Merge
on:
  pull_request:
    types: [closed]
    branches: [main]
jobs:
  post-merge:
    if: github.event.pull_request.merged == true
    runs-on: ubuntu-latest
    steps:
      - name: Update Jira Status
        run: |
          # Extract REIP number from PR title
          # Call Jira API to update status to Done
          # Add PR link to Jira issue
      - name: Deploy to Staging
        run: |
          # Trigger staging deployment
      - name: Notify Team
        run: |
          # Send Slack/Teams notification
```

### Branch Protection Rules

**Required Configuration for Auto-Merge:**

```json
{
  "required_status_checks": {
    "strict": true,
    "contexts": [
      "build-and-test",
      "security-scan"
    ]
  },
  "enforce_admins": true,
  "required_pull_request_reviews": {
    "required_approving_review_count": 1,
    "dismiss_stale_reviews": true,
    "require_code_owner_reviews": false
  },
  "restrictions": null,
  "allow_auto_merge": true,
  "allow_squash_merge": true,
  "allow_merge_commit": false,
  "allow_rebase_merge": false,
  "delete_branch_on_merge": true
}
```

---

## Quick Reference Commands

### Start New Feature

```bash
# 1. Assign issue in Jira and move to "In Development"
# 2. Create feature branch
git checkout main && git pull origin main
git checkout -b feature/reip-{number}-{description}
git push -u origin feature/reip-{number}-{description}
```

### Create Pull Request

```bash
# 1. Ensure all changes committed and pushed
git push origin feature/reip-{number}-{description}

# 2. Create PR with auto-merge enabled
gh pr create --title "feat(REIP-{number}): {title}" --body-file pr-template.md
gh pr merge --auto --squash

# 3. Monitor auto-merge status
gh pr checks
```

### Complete Automated Workflow

```bash
# 1. Auto-merge handles merge when approved and checks pass
# 2. GitHub Actions handle post-merge automation:
#    - Branch deletion
#    - Jira status update to Done
#    - Staging deployment
#    - Team notifications

# 3. Manual verification (if needed)
git checkout main && git pull origin main

# 4. Verify Jira status updated automatically
# 5. Verify staging deployment completed
```

---

## Troubleshooting Common Issues

### Issue: "Auto-merge not available"

**Solution**: Verify branch protection rules and required checks

```bash
# Check branch protection status
gh api repos/:owner/:repo/branches/main/protection

# Verify required status checks are passing
gh pr checks

# Enable auto-merge manually
gh pr merge --auto --squash
```

### Issue: "Branch protection rules prevent merge"

**Solution**: Ensure all required checks pass (build, tests, reviews)

### Issue: "Merge conflicts with main"

**Solution**:

```bash
git checkout feature/your-branch
git rebase main
# Resolve conflicts
git push --force-with-lease origin feature/your-branch
```

### Issue: "Jira status not updated automatically"

**Solution**:

```bash
# Check webhook configuration
./scripts/automation/Verify-Webhook-Integration.ps1

# Manual update fallback
./scripts/jira/Update-Issue-Status.ps1 -IssueKey "REIP-{number}" -Status "Done"
```

### Issue: "Auto-merge failed after approval"

**Solution**:

```bash
# Check if all required checks passed
gh pr checks

# Verify branch is up-to-date
git checkout feature/reip-{number}-{description}
git rebase main
git push --force-with-lease

# Re-enable auto-merge
gh pr merge --auto --squash
```

### Issue: "GitHub Actions workflow failed"

**Solution**:

```bash
# Check workflow run logs
gh run list --workflow=ci.yml
gh run view {run-id} --log

# Re-run failed workflow
gh run rerun {run-id}
```

### Issue: "Jira API authentication failed"

**Solution**: Run `scripts/jira/Set-PersistentJiraEnvironmentVariables.ps1`

---

## Workflow Checklist Template

Copy this checklist for each new development task:

### Pre-Development

- [ ] Issue assigned in Jira
- [ ] Issue moved to "In Development"
- [ ] Requirements and acceptance criteria reviewed
- [ ] Feature branch created from latest main
- [ ] Development environment verified

### During Development

- [ ] Code follows project standards
- [ ] Tests added for new functionality
- [ ] Build passes locally
- [ ] Security considerations addressed
- [ ] Documentation updated

### Pre-PR

- [ ] All changes committed with conventional commit messages
- [ ] Feature branch pushed to GitHub
- [ ] Build passes in CI
- [ ] Tests pass
- [ ] No merge conflicts with main

### PR Process

- [ ] PR created with comprehensive description
- [ ] Auto-merge enabled for approved PRs
- [ ] Reviewers assigned
- [ ] Build/test status checks pass
- [ ] Code review completed and approved
- [ ] PR auto-merged using "Squash and merge"

### Post-Merge (Automated)

- [ ] Feature branch automatically deleted
- [ ] Local main branch updated manually
- [ ] Jira issue automatically moved to "Done"
- [ ] Staging deployment automatically triggered
- [ ] Team notifications sent automatically
- [ ] Manual verification of automation completion

---

**Remember: This workflow exists to ensure quality, maintainability, and team collaboration. Following it consistently leads to better software and fewer production issues.**
