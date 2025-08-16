---
applyTo: "**"
---

# Development Workflow **Identity Validation Checklist:**

- [ ] Git user.email = `copilotwhittenberger@gmail.com`
- [ ] Git user.name = "Copilot Engineer"
- [ ] NO work performed under `kwhittenberger@mac.com` identity
- [ ] Identity verified before each development sessionctions

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

#### 1.1 Identity Verification (MANDATORY FIRST STEP)

```bash
# ✅ CRITICAL: Verify Git identity before any development work
git config --get user.email
git config --get user.name

# ✅ REQUIRED: Must show copilotwhittenberger@gmail.com and "Copilot Engineer"
# ❌ STOP: If showing kwhittenberger@mac.com or any other identity
```

**Identity Configuration Requirements:**

```bash
# ✅ REQUIRED: Set correct identity if not already configured
git config user.email "copilotwhittenberger@gmail.com"
git config user.name "Copilot Engineer"

# ✅ VERIFY: Confirm configuration is correct
git config --list | grep user
```

**Identity Validation Checklist:**

- [ ] Git user.email = <copilotwhittenberger@gmail.com>
- [ ] Git user.name = "Copilot Engineer"
- [ ] NO work performed under <kwhittenberger@mac.com> identity
- [ ] Identity verified before each development session

#### 1.2 Jira Issue Management

```bash
# ✅ REQUIRED: Assign issue to copilotwhittenberger@gmail.com (Copilot Engineer)
# ✅ REQUIRED: Move issue from "Backlog" to "In Development"
# ✅ REQUIRED: Verify Epic assignment and sprint assignment
```

**Validation Checklist:**

- [ ] **IDENTITY VERIFIED** (see 1.1 above)
- [ ] **REQUIRED**: Use manage_todo_list tool to create initial todo list for the task
- [ ] Issue assigned to `copilotwhittenberger@gmail.com` (Copilot Engineer)
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

- [ ] **REQUIRED**: Use manage_todo_list tool to mark items as in-progress before starting work
- [ ] **REQUIRED**: Use manage_todo_list tool to mark items as completed immediately after finishing
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
# ✅ REQUIRED: Code formatting verification
dotnet format --verify-no-changes

# ✅ REQUIRED: Build verification
dotnet build

# ✅ REQUIRED: Test execution with UNIFIED FRAMEWORK
dotnet test

# ✅ REQUIRED: Unified test framework validation
# Verify all test projects use RealEstatePlatform.Testing library
dotnet list package --include-transitive | grep RealEstatePlatform.Testing

# ✅ REQUIRED: Code quality checks
# Run linting, static analysis, security scans
```

**Validation Checklist:**

- [ ] Code formatting passes (`dotnet format --verify-no-changes`)
- [ ] All builds pass successfully
- [ ] **MANDATORY**: All tests use unified RealEstatePlatform.Testing library
- [ ] **MANDATORY**: No custom test infrastructure implementations present
- [ ] **MANDATORY**: All test data creation uses builder patterns
- [ ] All tests pass with unified framework
- [ ] No security vulnerabilities introduced
- [ ] Code follows project conventions
- [ ] Documentation updated if needed

**Testing Framework Compliance (MANDATORY):**

- [ ] **REQUIRED**: All test projects reference `RealEstatePlatform.Testing`
- [ ] **PROHIBITED**: Custom WebApplicationFactory implementations
- [ ] **PROHIBITED**: Manual database context setup/cleanup
- [ ] **PROHIBITED**: Custom authentication helpers
- [ ] **PROHIBITED**: Direct entity instantiation (must use builders)
- [ ] **REQUIRED**: Use `DatabaseFixture` for database tests
- [ ] **REQUIRED**: Use `AuthenticationFixture` for auth tests
- [ ] **REQUIRED**: Use `TestWebApplicationFactory` for integration tests
- [ ] **REQUIRED**: Use builder patterns for all test data

### Phase 4: Pull Request Creation

#### 4.1 Pre-PR Checklist

- [ ] Code formatting verified (`dotnet format --verify-no-changes`)
- [ ] All changes committed and pushed
- [ ] Feature branch up to date with main
- [ ] Build passes successfully
- [ ] Tests pass
- [ ] Documentation updated

#### 4.2 PR Creation Process

```bash
# ✅ REQUIRED: Push latest changes
git push origin feature/reip-{issue-number}-{description}

# ✅ REQUIRED: Create PR using GitHub CLI with detailed description
gh pr create \
  --title "feat(REIP-{number}): {Implementation Title}" \
  --body-file pr-template.md \
  --assignee copilotwhittenberger@gmail.com \
  --label "enhancement" \
  --milestone "Sprint 1"

# ✅ RECOMMENDED: Enable manual auto-merge after PR is ready
# Wait for: reviewers assigned, all checks passing, approval received
gh pr merge <PR_NUMBER> --auto --squash --delete-branch
```

#### 4.2.1 Auto-Merge Configuration

**Prerequisites for Auto-Merge:**

- Branch protection rules configured on main branch
- Required status checks enabled (build, tests, security)
- Required reviewers configured (minimum 1)
- Dismiss stale reviews enabled

**Manual Auto-Merge (Recommended Approach):**

Due to branch protection settings with `enforce_admins: true`, GitHub Actions cannot automatically enable auto-merge. Use the manual approach:

```bash
# After PR creation and when ready to merge:
gh pr merge <PR_NUMBER> --auto --squash --delete-branch

# Check PR status and requirements
gh pr checks <PR_NUMBER>
gh pr view <PR_NUMBER> --json mergeable,mergeStateStatus
```

**Automated Auto-Merge (Limited Support):**

GitHub Actions auto-merge may fail with branch protection `enforce_admins: true`. Only works when this setting is disabled:

```bash
# This approach requires enforce_admins: false in branch protection
gh pr merge --auto --squash
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

- [ ] **MANDATORY**: All tests use RealEstatePlatform.Testing unified library
- [ ] **MANDATORY**: No custom test infrastructure implementations
- [ ] **MANDATORY**: All test data creation uses builder patterns
- [ ] **MANDATORY**: Database tests use DatabaseFixture from unified library
- [ ] **MANDATORY**: Authentication tests use AuthenticationFixture from unified library
- [ ] **MANDATORY**: Integration tests use TestWebApplicationFactory from unified library
- [ ] Adequate test coverage for new functionality
- [ ] Tests are meaningful and robust
- [ ] Edge cases covered
- [ ] Integration points tested
- [ ] All tests pass with unified framework

**Unified Testing Framework Compliance:**

- [ ] **ZERO TOLERANCE**: No custom WebApplicationFactory implementations
- [ ] **ZERO TOLERANCE**: No manual database setup/cleanup patterns
- [ ] **ZERO TOLERANCE**: No custom authentication helpers
- [ ] **ZERO TOLERANCE**: No direct entity instantiation (must use builders)
- [ ] **ZERO TOLERANCE**: No duplicate test infrastructure patterns
- [ ] **REQUIRED**: Use collection fixtures (`[Collection("Database")]`, `[Collection("Authentication")]`)
- [ ] **REQUIRED**: Follow established builder patterns (UserBuilder, PropertyBuilder, TestDataBuilder)
- [ ] **REQUIRED**: Proper async/await patterns in test methods

**Documentation:**

- [ ] Public APIs documented
- [ ] Complex logic commented
- [ ] README updates if needed
- [ ] Architecture decisions recorded

### Phase 6: Handoff

#### 6.1 Manual Merge Process (Recommended)

**Manual Auto-Merge (Primary Approach):**

Due to branch protection `enforce_admins: true`, use manual auto-merge for reliable merging:

```bash
# ✅ RECOMMENDED: Manual auto-merge when PR is ready
gh pr merge <PR_NUMBER> --auto --squash --delete-branch

# Verify PR requirements are met
gh pr checks <PR_NUMBER>
gh pr view <PR_NUMBER> --json mergeable,mergeStateStatus

# Update local main branch after merge
git checkout main
git pull origin main
```

**Direct Manual Merge (Fallback):**

```bash
# ✅ FALLBACK: Use GitHub web interface or CLI for immediate merge
# In GitHub web interface: Use "Squash and merge" button
# Or via CLI when auto-merge is not needed:
gh pr merge <PR_NUMBER> --squash --delete-branch
```

#### 6.2 Automated Post-Merge Actions

**GitHub Actions Automation (Triggered on Merge):**

- [ ] **Branch cleanup** - Automatic feature branch deletion
- [ ] **GitHub issue closure** - Via `Closes #` syntax in PR description
- [ ] **Deployment trigger** - Staging environment deployment
- [ ] **Jira status update** - Via webhook integration
- [ ] **Notification dispatch** - Team notifications via Slack/Teams

**Manual Post-Merge Actions (If Automation Fails):**

- [ ] **REQUIRED**: Use manage_todo_list tool to ensure all todos are marked completed
- [ ] **Verify Jira status** updated to "Done"
- [ ] **Add completion comment** in Jira with PR link using `.\scripts\jira\Add-JiraComment.ps1`
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
# Update issue status using standardized CRUD operations
# Note: When moving to "Done" status, the issue is automatically unassigned
.\scripts\jira\Set-JiraIssue.ps1 -IssueKey "REIP-{number}" -Status "Done"

# To override auto-unassignment (rare cases), explicitly specify assignee
.\scripts\jira\Set-JiraIssue.ps1 -IssueKey "REIP-{number}" -Status "Done" -Assignee "user@example.com"

# Add completion comment with PR link using dedicated comment script
.\scripts\jira\Add-JiraComment.ps1 -IssueKey "REIP-{number}" -Comment "Completed via PR: https://github.com/kwhittenberger/real-estate-requirements/pull/{pr-number}"
```

**Auto-Unassignment Policy:**

- **Automatic**: Moving any issue to "Done" status automatically unassigns it
- **Override**: Explicitly specify `-Assignee` parameter to override this behavior
- **Rationale**: Completed tasks should be unassigned to allow team focus on active work

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

- `scripts/jira/New-JiraIssue.ps1` - Create new issues with comprehensive parameters
- `scripts/jira/Set-JiraIssue.ps1` - Update issue status and fields
- `scripts/jira/Get-JiraIssue.ps1` - Retrieve and search issues
- `scripts/jira/Add-JiraComment.ps1` - Add comments to issues with formatting options
- `scripts/jira/Remove-JiraIssue.ps1` - Delete issues with confirmations
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
# 1. Assign issue to copilotwhittenberger@gmail.com in Jira and move to "In Progress"
# 2. Create feature branch
git checkout main && git pull origin main
git checkout -b feature/reip-{number}-{description}
git push -u origin feature/reip-{number}-{description}
```

### Create Pull Request

```bash
# 1. Ensure all changes committed and pushed
git push origin feature/reip-{number}-{description}

# 2. Create PR with comprehensive description
gh pr create --title "feat(REIP-{number}): {title}" --body-file pr-template.md

# 3. Enable auto-merge manually (after creation)
gh pr merge <PR_NUMBER> --auto --squash --delete-branch

# 4. Monitor PR status
gh pr checks <PR_NUMBER>
```

### Complete Automated Workflow

```bash
# 1. Manual auto-merge handles merge when approved and checks pass
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

### Issue: "GitHub Actions auto-merge permissions error"

**Root Cause**: Branch protection `enforce_admins: true` prevents GitHub Actions from enabling auto-merge

**Solution**: Use manual auto-merge approach

```bash
# Manual auto-merge (recommended approach)
gh pr merge <PR_NUMBER> --auto --squash --delete-branch

# Check PR status first
gh pr checks <PR_NUMBER>
gh pr view <PR_NUMBER> --json mergeable,mergeStateStatus
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

### Issue: "Jira script not found"

**Solution**: Use standardized CRUD operations:

```powershell
# Instead of obsolete scripts, use:
.\scripts\jira\New-JiraIssue.ps1      # For creating issues
.\scripts\jira\Get-JiraIssue.ps1      # For retrieving issues  
.\scripts\jira\Set-JiraIssue.ps1      # For updating issues
.\scripts\jira\Add-JiraComment.ps1    # For adding comments
.\scripts\jira\Remove-JiraIssue.ps1   # For deleting issues
```

---

## Workflow Checklist Template

Copy this checklist for each new development task:

### Pre-Development

- [ ] Issue assigned to <copilotwhittenberger@gmail.com> in Jira
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
- [ ] Manual auto-merge enabled when PR is ready for approval
- [ ] Reviewers assigned
- [ ] Build/test status checks pass
- [ ] Code review completed and approved
- [ ] PR manually merged using `gh pr merge --auto --squash --delete-branch`

### Post-Merge (Automated)

- [ ] Feature branch automatically deleted via manual auto-merge
- [ ] Local main branch updated manually
- [ ] Jira issue automatically moved to "Done"
- [ ] Staging deployment automatically triggered
- [ ] Team notifications sent automatically
- [ ] Manual verification of automation completion

---

**Remember: This workflow exists to ensure quality, maintainability, and team collaboration. Following it consistently leads to better software and fewer production issues.**
