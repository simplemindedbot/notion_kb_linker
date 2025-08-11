# GitHub Project Setup Guide

This guide provides step-by-step instructions for setting up the GitHub repository with proper labels, milestones, and initial issues based on the product backlog.

## Prerequisites

1. GitHub repository created: `notion_kb_linker`
2. GitHub CLI installed and authenticated: `gh auth login`
3. Repository cloned locally with proper permissions

## Step 1: Create GitHub Labels

Run the label creation commands from `.github/LABELS.md`:

```bash
# Navigate to project directory
cd /path/to/notion_kb_linker

# Create all labels (copy commands from .github/LABELS.md)
# Type labels
gh label create "enhancement" --color "7057ff" --description "New feature or enhancement request"
gh label create "bug" --color "d73a4a" --description "Something isn't working correctly"
gh label create "user-story" --color "0052cc" --description "User story for development"
gh label create "task" --color "5319e7" --description "Technical task or subtask"
gh label create "documentation" --color "0075ca" --description "Documentation improvements"

# Priority labels
gh label create "priority-critical" --color "b60205" --description "Must be fixed immediately"
gh label create "priority-high" --color "d93f0b" --description "Important, should be addressed soon"
gh label create "priority-medium" --color "fbca04" --description "Normal priority"
gh label create "priority-low" --color "0e8a16" --description "Can be deferred if needed"

# Continue with all other labels from LABELS.md...
```

## Step 2: Create Milestones

```bash
# Create release milestones (adjust dates as needed)
gh api repos/simplemindedbot/notion_kb_linker/milestones \
  -f title="v1.0-alpha (MVP)" \
  -f description="Minimum Viable Product with core functionality" \
  -f due_on="2025-09-22T23:59:59Z"

gh api repos/simplemindedbot/notion_kb_linker/milestones \
  -f title="v1.0-beta (Feature Complete)" \
  -f description="Feature-complete version with enhanced UX" \
  -f due_on="2025-10-20T23:59:59Z"

gh api repos/simplemindedbot/notion_kb_linker/milestones \
  -f title="v1.0 (Production)" \
  -f description="Production-ready release" \
  -f due_on="2025-11-03T23:59:59Z"

# Create sprint milestones
gh api repos/simplemindedbot/notion_kb_linker/milestones \
  -f title="Sprint 1: Foundation" \
  -f description="Core infrastructure and database integration" \
  -f due_on="2025-08-25T23:59:59Z"

# Continue with other sprint milestones...
```

## Step 3: Create Initial Issues from Product Backlog

### Epic 1: Foundation and Database Integration

#### US-001: Initial Database Connection
```bash
gh issue create \
  --title "[STORY] Initial Database Connection" \
  --body "**Epic**: Epic 1: Foundation and Database Integration

**User Story**: As a knowledge manager, I want to connect to my Notion Knowledge Base database so that the system can analyze my content and suggest improvements.

**Acceptance Criteria**:
- Given valid Notion integration token and database ID
- When I run the connection command  
- Then system authenticates successfully and displays database info
- And system shows page count and basic statistics
- And connection errors are clearly explained with resolution steps

**Story Points**: 3
**Priority**: Must-have (MVP)
**Dependencies**: None

**Technical Notes**: Implement Notion API client with proper error handling" \
  --label "user-story,component-database,priority-high,epic-foundation,release-mvp,size-m,needs-estimation" \
  --milestone "Sprint 1: Foundation"
```

#### US-002: Environment and Configuration Setup
```bash
gh issue create \
  --title "[STORY] Environment and Configuration Setup" \
  --body "**Epic**: Epic 1: Foundation and Database Integration

**User Story**: As a developer, I want a robust configuration system so that the application can be easily customized for different environments and use cases.

**Acceptance Criteria**:
- Given various deployment scenarios
- When configuration is loaded
- Then system reads from environment variables, config files, and CLI args
- And configuration validation provides clear error messages
- And default values are applied appropriately
- And sensitive data is handled securely

**Story Points**: 5
**Priority**: Must-have (MVP)
**Dependencies**: None

**Technical Notes**: Support YAML/JSON config files, environment variable validation" \
  --label "user-story,component-config,priority-high,epic-foundation,release-mvp,size-l,needs-estimation" \
  --milestone "Sprint 1: Foundation"
```

### Continue creating issues for each user story...

## Step 4: Set Up Project Boards (Optional)

Create a project board for better visual management:

```bash
# Create project board
gh api user/projects -f name="Notion KB Auto-Linker" -f body="Product development tracking"

# Add columns (requires project ID from previous command)
# Backlog, Sprint Planning, In Progress, Review, Testing, Done
```

## Step 5: Enable Repository Features

### Enable Discussions
```bash
gh api repos/simplemindedbot/notion_kb_linker -f has_discussions=true
```

### Set up Branch Protection (after initial development)
```bash
gh api repos/simplemindedbot/notion_kb_linker/branches/main/protection \
  -f required_status_checks='{"strict":true,"contexts":["ci/test","ci/lint"]}' \
  -f enforce_admins=true \
  -f required_pull_request_reviews='{"required_approving_review_count":1}' \
  -f restrictions=null
```

## Step 6: Create Detailed Issues Script

Here's a bash script to create all user stories from the product backlog:

```bash
#!/bin/bash
# create_issues.sh - Create all user stories from product backlog

# Epic 1: Foundation and Database Integration
echo "Creating Epic 1 issues..."

gh issue create \
  --title "[STORY] US-001: Initial Database Connection" \
  --body-file "./scripts/issues/us-001.md" \
  --label "user-story,component-database,priority-high,epic-foundation,release-mvp,size-m" \
  --milestone "Sprint 1: Foundation"

gh issue create \
  --title "[STORY] US-002: Environment and Configuration Setup" \
  --body-file "./scripts/issues/us-002.md" \
  --label "user-story,component-config,priority-high,epic-foundation,release-mvp,size-l" \
  --milestone "Sprint 1: Foundation"

gh issue create \
  --title "[STORY] US-003: Basic Error Handling and Logging" \
  --body-file "./scripts/issues/us-003.md" \
  --label "user-story,component-cli,priority-high,epic-foundation,release-mvp,size-m" \
  --milestone "Sprint 1: Foundation"

gh issue create \
  --title "[STORY] US-004: Content Extraction Pipeline" \
  --body-file "./scripts/issues/us-004.md" \
  --label "user-story,component-database,priority-high,epic-foundation,release-mvp,size-l" \
  --milestone "Sprint 1: Foundation"

# Epic 2: Content Analysis and Semantic Processing
echo "Creating Epic 2 issues..."

gh issue create \
  --title "[STORY] US-005: Text Processing and Cleaning" \
  --body-file "./scripts/issues/us-005.md" \
  --label "user-story,component-analysis,priority-high,epic-analysis,release-mvp,size-m" \
  --milestone "Sprint 2: Analysis Engine"

gh issue create \
  --title "[STORY] US-006: Semantic Embedding Generation" \
  --body-file "./scripts/issues/us-006.md" \
  --label "user-story,component-analysis,priority-high,epic-analysis,release-mvp,size-l" \
  --milestone "Sprint 2: Analysis Engine"

gh issue create \
  --title "[STORY] US-007: Similarity Matrix Calculation" \
  --body-file "./scripts/issues/us-007.md" \
  --label "user-story,component-analysis,priority-high,epic-analysis,release-mvp,size-l" \
  --milestone "Sprint 2: Analysis Engine"

gh issue create \
  --title "[STORY] US-008: Content Analysis Caching System" \
  --body-file "./scripts/issues/us-008.md" \
  --label "user-story,component-analysis,priority-medium,epic-analysis,release-mvp,size-l" \
  --milestone "Sprint 3: Recommendations"

# Epic 3: Safety and Backup Systems
echo "Creating Epic 3 issues..."

gh issue create \
  --title "[STORY] US-009: Comprehensive Backup System" \
  --body-file "./scripts/issues/us-009.md" \
  --label "user-story,component-backup,priority-critical,epic-safety,release-mvp,size-l" \
  --milestone "Sprint 1: Foundation"

gh issue create \
  --title "[STORY] US-010: Dry Run Preview System" \
  --body-file "./scripts/issues/us-010.md" \
  --label "user-story,component-backup,priority-high,epic-safety,release-mvp,size-l" \
  --milestone "Sprint 2: Analysis Engine"

gh issue create \
  --title "[STORY] US-011: Change Tracking Database" \
  --body-file "./scripts/issues/us-011.md" \
  --label "user-story,component-backup,priority-medium,epic-safety,release-v1.0,size-m" \
  --milestone "Sprint 4: Enhanced UX"

# Epic 4: Tag Generation and Management
echo "Creating Epic 4 issues..."

gh issue create \
  --title "[STORY] US-012: NLP-Based Tag Generation" \
  --body-file "./scripts/issues/us-012.md" \
  --label "user-story,component-tags,priority-high,epic-tags,release-mvp,size-l" \
  --milestone "Sprint 2: Analysis Engine"

gh issue create \
  --title "[STORY] US-013: Tag Quality Control and Review" \
  --body-file "./scripts/issues/us-013.md" \
  --label "user-story,component-tags,priority-medium,epic-tags,release-v1.0,size-l" \
  --milestone "Sprint 3: Recommendations"

gh issue create \
  --title "[STORY] US-014: Enhanced Tag Generation with LLM" \
  --body-file "./scripts/issues/us-014.md" \
  --label "user-story,component-tags,priority-low,epic-tags,release-future,size-m" \
  --milestone "Sprint 5: Quality & Polish"

# Epic 5: Cross-Link Discovery and Creation
echo "Creating Epic 5 issues..."

gh issue create \
  --title "[STORY] US-015: Link Recommendation Engine" \
  --body-file "./scripts/issues/us-015.md" \
  --label "user-story,component-links,priority-high,epic-links,release-mvp,size-xl" \
  --milestone "Sprint 3: Recommendations"

gh issue create \
  --title "[STORY] US-016: Intelligent Link Placement" \
  --body-file "./scripts/issues/us-016.md" \
  --label "user-story,component-links,priority-medium,epic-links,release-v1.0,size-xl" \
  --milestone "Sprint 4: Enhanced UX"

gh issue create \
  --title "[STORY] US-017: Link Quality Assessment" \
  --body-file "./scripts/issues/us-017.md" \
  --label "user-story,component-links,priority-low,epic-links,release-future,size-s" \
  --milestone "Sprint 5: Quality & Polish"

# Epic 6: User Experience and Workflow Management
echo "Creating Epic 6 issues..."

gh issue create \
  --title "[STORY] US-018: CLI Interface with Rich Formatting" \
  --body-file "./scripts/issues/us-018.md" \
  --label "user-story,component-cli,priority-medium,epic-ux,release-mvp,size-l" \
  --milestone "Sprint 3: Recommendations"

gh issue create \
  --title "[STORY] US-019: Flexible Approval Workflows" \
  --body-file "./scripts/issues/us-019.md" \
  --label "user-story,component-cli,priority-medium,epic-ux,release-v1.0,size-xl" \
  --milestone "Sprint 4: Enhanced UX"

gh issue create \
  --title "[STORY] US-020: Advanced Configuration Management" \
  --body-file "./scripts/issues/us-020.md" \
  --label "user-story,component-config,priority-medium,epic-ux,release-v1.0,size-m" \
  --milestone "Sprint 4: Enhanced UX"

gh issue create \
  --title "[STORY] US-021: Rollback and Recovery System" \
  --body-file "./scripts/issues/us-021.md" \
  --label "user-story,component-backup,priority-medium,epic-ux,release-v1.0,size-m" \
  --milestone "Sprint 5: Quality & Polish"

echo "All issues created successfully!"
```

## Step 7: Issue Body Templates

Create individual markdown files for each user story in `scripts/issues/`:

### Example: us-001.md
```markdown
## Epic
Epic 1: Foundation and Database Integration

## User Story
As a knowledge manager, I want to connect to my Notion Knowledge Base database so that the system can analyze my content and suggest improvements.

## Detailed Description
This story establishes the foundation for all subsequent functionality by implementing secure, reliable connection to Notion databases. The implementation must handle authentication, basic database queries, and provide meaningful feedback about the connection status and database characteristics.

## Acceptance Criteria
- **Given** valid Notion integration token and database ID
- **When** I run the connection command
- **Then** system authenticates successfully and displays database information
- **And** system shows page count and basic statistics about the database
- **And** connection errors are clearly explained with resolution steps
- **And** system validates token permissions and database access rights

## Technical Requirements
- Use `notion-client` library for official API integration
- Implement proper error handling for authentication failures
- Support environment variable and config file credential management
- Provide detailed logging for troubleshooting connection issues
- Handle rate limiting with appropriate backoff strategies

## Business Value
Establishes the foundational capability that enables all content analysis and enhancement features. Without reliable database connection, no other functionality is possible.

## Dependencies
- None (foundational story)

## Story Points
3 (Medium complexity - 1 day of work)

## Definition of Done
- [ ] Notion API integration implemented and tested
- [ ] Authentication error handling with clear user messages
- [ ] Database information display working correctly
- [ ] Configuration system supports multiple credential sources
- [ ] Unit tests covering happy path and error conditions
- [ ] Integration tests with actual Notion API (using test database)
- [ ] Documentation updated with setup and troubleshooting guides
- [ ] Code follows project standards and passes all quality checks
```

## Step 8: Verification Checklist

After setup, verify:

- [ ] All labels are created with correct colors and descriptions
- [ ] All milestones are created with proper dates
- [ ] All user stories are created with appropriate labels and milestones
- [ ] Issue templates are working correctly
- [ ] Repository settings are configured (discussions, branch protection)
- [ ] Project board is set up (if using)
- [ ] Documentation references are correct in issue templates

## Step 9: Team Onboarding

Share with team members:
1. Link to requirements documentation
2. Link to product backlog
3. GitHub project setup and workflow
4. Issue creation and labeling guidelines
5. Sprint planning process and ceremonies

## Maintenance Tasks

### Weekly
- Review and triage new issues
- Update story points and priorities based on learnings
- Adjust milestone dates if needed

### Sprint Boundaries  
- Close completed milestones
- Create new milestones for future sprints
- Review and update issue priorities
- Archive completed issues

### Release Preparation
- Update documentation references
- Verify all acceptance criteria are met
- Create release notes from closed issues
- Plan next release milestones

This setup provides a solid foundation for agile development with clear tracking, proper categorization, and comprehensive documentation.