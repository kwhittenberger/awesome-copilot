---
mode: 'agent'
description: 'Create Jira Issues from implementation plan phases using appropriate Jira automation scripts.'
tools: ['codebase', 'search', 'run_in_terminal']
---
# Create Jira Issues from Implementation Plan

Create Jira Issues for the implementation plan at `${file}`.

## Process

1. Analyze plan file to identify phases
2. Check existing issues in Jira
3. Create new Jira issues per phase using appropriate automation scripts
4. Use proper Jira Story or Task templates with ADF formatting

## Requirements

- One Jira issue per implementation phase
- Clear, structured summaries and descriptions in ADF format
- Include only changes required by the plan
- Verify against existing Jira issues before creation
- Use appropriate Epic linkage and story points

## Issue Content

- Summary: Phase name from implementation plan
- Description: Phase details, requirements, and context in ADF format
- Issue Type: Story or Task as appropriate
- Epic Link: Link to appropriate Epic if applicable

**Note**: All issues MUST be created in Jira, not GitHub Issues.
