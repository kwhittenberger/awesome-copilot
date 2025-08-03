---
mode: 'agent'
description: 'Create Jira Issues for unimplemented requirements from specification files using appropriate Jira automation scripts.'
tools: ['codebase', 'search', 'run_in_terminal']
---
# Create Jira Issues for Unmet Specification Requirements

Create Jira Issues for unimplemented requirements in the specification at `${file}`.

## Process

1. Analyze specification file to extract all requirements
2. Check codebase implementation status for each requirement
3. Check existing Jira issues to avoid duplicates
4. Create new Jira issue per unimplemented requirement using automation scripts
5. Use proper Jira Story template with ADF formatting

## Requirements

- One Jira issue per unimplemented requirement from specification
- Clear requirement ID and description mapping in ADF format
- Include implementation guidance and acceptance criteria
- Verify against existing Jira issues before creation
- Use appropriate Epic linkage and story points

## Issue Content

- Summary: Requirement ID and brief description
- Description: Detailed requirement, implementation method, and context in ADF format
- Issue Type: Story or Task as appropriate
- Epic Link: Link to appropriate Epic if applicable

## Implementation Check

- Search codebase for related code patterns
- Check related specification files in `/spec/` directory
- Verify requirement isn't partially implemented

**Note**: All issues MUST be created in Jira, not GitHub Issues.
