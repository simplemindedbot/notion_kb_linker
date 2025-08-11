# GitHub Labels Configuration

This document defines the label system for the Notion KB Auto-Linker project.

## Label Categories and Structure

### Type Labels (What kind of work)
| Label | Color | Description |
|-------|--------|-------------|
| `enhancement` | #7057ff | New feature or enhancement request |
| `bug` | #d73a4a | Something isn't working correctly |
| `user-story` | #0052cc | User story for development |
| `task` | #5319e7 | Technical task or subtask |
| `documentation` | #0075ca | Documentation improvements |
| `question` | #d876e3 | Further information is requested |

### Priority Labels (How important)
| Label | Color | Description |
|-------|--------|-------------|
| `priority-critical` | #b60205 | Must be fixed immediately |
| `priority-high` | #d93f0b | Important, should be addressed soon |
| `priority-medium` | #fbca04 | Normal priority |
| `priority-low` | #0e8a16 | Can be deferred if needed |

### Status Labels (Where we are)
| Label | Color | Description |
|-------|--------|-------------|
| `needs-triage` | #f9d0c4 | Needs initial review and categorization |
| `needs-investigation` | #d4c5f9 | Requires research or investigation |
| `needs-estimation` | #c2e0c6 | Needs story points or effort estimation |
| `ready-for-dev` | #c5f0d8 | Ready for development work |
| `in-progress` | #fef2c0 | Currently being worked on |
| `waiting-review` | #bfd4f2 | Waiting for code review |
| `waiting-testing` | #f1d8c9 | Ready for testing |
| `blocked` | #e99695 | Cannot proceed due to blocker |

### Component Labels (Which part of system)
| Label | Color | Description |
|-------|--------|-------------|
| `component-database` | #006b75 | Database connection and integration |
| `component-analysis` | #0e4b99 | Content analysis and NLP |
| `component-tags` | #5a32a3 | Tag generation and management |
| `component-links` | #d1242f | Cross-link recommendation |
| `component-backup` | #b08800 | Backup and safety systems |
| `component-cli` | #040f3e | Command-line interface |
| `component-config` | #5d2f7a | Configuration management |

### Epic Labels (Which major feature area)
| Label | Color | Description |
|-------|--------|-------------|
| `epic-foundation` | #1f4e79 | Foundation and Database Integration |
| `epic-analysis` | #2e7d32 | Content Analysis and Semantic Processing |
| `epic-safety` | #d84315 | Safety and Backup Systems |
| `epic-tags` | #7b1fa2 | Tag Generation and Management |
| `epic-links` | #c62828 | Cross-Link Discovery and Creation |
| `epic-ux` | #f57f17 | User Experience and Workflow Management |

### Release Labels (Which version)
| Label | Color | Description |
|-------|--------|-------------|
| `release-mvp` | #2ea043 | MVP release (v1.0-alpha) |
| `release-v1.0` | #1a7f37 | Full v1.0 release |
| `release-future` | #656d76 | Future release consideration |

### Size Labels (How much work - Story Points)
| Label | Color | Description |
|-------|--------|-------------|
| `size-xs` | #f0f9ff | 1 story point (few hours) |
| `size-s` | #dbeafe | 2 story points (half day) |
| `size-m` | #93c5fd | 3 story points (1 day) |
| `size-l` | #60a5fa | 5 story points (2-3 days) |
| `size-xl` | #3b82f6 | 8 story points (1 week) |
| `size-xxl` | #1d4ed8 | 13+ story points (needs breakdown) |

### Special Labels
| Label | Color | Description |
|-------|--------|-------------|
| `good-first-issue` | #7057ff | Good for newcomers |
| `help-wanted` | #008672 | Extra attention is needed |
| `duplicate` | #cfd3d7 | Duplicate of another issue |
| `wont-fix` | #ffffff | This will not be worked on |
| `breaking-change` | #d73a4a | Contains breaking changes |
| `security` | #d73a4a | Security-related issue |

## Label Usage Guidelines

### Mandatory Labels for Issues
Every issue should have at least:
- One **Type** label (bug, enhancement, user-story, task)
- One **Component** label (which part of system)
- One **Priority** label (unless it's a question)
- One **Status** label (starts with needs-triage)

### Epic and Release Planning
- Use **Epic** labels for organizing related work
- Use **Release** labels for release planning
- Use **Size** labels for story point estimation

### Workflow Status Progression
Typical status progression:
1. `needs-triage` → Initial issue created
2. `needs-investigation` → Needs research (optional)
3. `needs-estimation` → Needs story points (for stories/tasks)
4. `ready-for-dev` → Ready to be worked on
5. `in-progress` → Development in progress
6. `waiting-review` → Code review needed
7. `waiting-testing` → Testing needed
8. **Closed** → Complete

### Automatic Label Rules

Consider setting up automation for:
- Add `needs-triage` to all new issues
- Add `component-*` labels based on file paths in PRs
- Add `breaking-change` when certain files are modified
- Add size labels based on PR complexity metrics

## Label Commands for GitHub CLI

Create all labels with these commands:

```bash
# Type labels
gh label create "enhancement" --color "7057ff" --description "New feature or enhancement request"
gh label create "bug" --color "d73a4a" --description "Something isn't working correctly"
gh label create "user-story" --color "0052cc" --description "User story for development"
gh label create "task" --color "5319e7" --description "Technical task or subtask"
gh label create "documentation" --color "0075ca" --description "Documentation improvements"
gh label create "question" --color "d876e3" --description "Further information is requested"

# Priority labels
gh label create "priority-critical" --color "b60205" --description "Must be fixed immediately"
gh label create "priority-high" --color "d93f0b" --description "Important, should be addressed soon"
gh label create "priority-medium" --color "fbca04" --description "Normal priority"
gh label create "priority-low" --color "0e8a16" --description "Can be deferred if needed"

# Status labels
gh label create "needs-triage" --color "f9d0c4" --description "Needs initial review and categorization"
gh label create "needs-investigation" --color "d4c5f9" --description "Requires research or investigation"
gh label create "needs-estimation" --color "c2e0c6" --description "Needs story points or effort estimation"
gh label create "ready-for-dev" --color "c5f0d8" --description "Ready for development work"
gh label create "in-progress" --color "fef2c0" --description "Currently being worked on"
gh label create "waiting-review" --color "bfd4f2" --description "Waiting for code review"
gh label create "waiting-testing" --color "f1d8c9" --description "Ready for testing"
gh label create "blocked" --color "e99695" --description "Cannot proceed due to blocker"

# Component labels
gh label create "component-database" --color "006b75" --description "Database connection and integration"
gh label create "component-analysis" --color "0e4b99" --description "Content analysis and NLP"
gh label create "component-tags" --color "5a32a3" --description "Tag generation and management"
gh label create "component-links" --color "d1242f" --description "Cross-link recommendation"
gh label create "component-backup" --color "b08800" --description "Backup and safety systems"
gh label create "component-cli" --color "040f3e" --description "Command-line interface"
gh label create "component-config" --color "5d2f7a" --description "Configuration management"

# Epic labels
gh label create "epic-foundation" --color "1f4e79" --description "Foundation and Database Integration"
gh label create "epic-analysis" --color "2e7d32" --description "Content Analysis and Semantic Processing"
gh label create "epic-safety" --color "d84315" --description "Safety and Backup Systems"
gh label create "epic-tags" --color "7b1fa2" --description "Tag Generation and Management"
gh label create "epic-links" --color "c62828" --description "Cross-Link Discovery and Creation"
gh label create "epic-ux" --color "f57f17" --description "User Experience and Workflow Management"

# Release labels
gh label create "release-mvp" --color "2ea043" --description "MVP release (v1.0-alpha)"
gh label create "release-v1.0" --color "1a7f37" --description "Full v1.0 release"
gh label create "release-future" --color "656d76" --description "Future release consideration"

# Size labels
gh label create "size-xs" --color "f0f9ff" --description "1 story point (few hours)"
gh label create "size-s" --color "dbeafe" --description "2 story points (half day)"
gh label create "size-m" --color "93c5fd" --description "3 story points (1 day)"
gh label create "size-l" --color "60a5fa" --description "5 story points (2-3 days)"
gh label create "size-xl" --color "3b82f6" --description "8 story points (1 week)"
gh label create "size-xxl" --color "1d4ed8" --description "13+ story points (needs breakdown)"

# Special labels
gh label create "good-first-issue" --color "7057ff" --description "Good for newcomers"
gh label create "help-wanted" --color "008672" --description "Extra attention is needed"
gh label create "duplicate" --color "cfd3d7" --description "Duplicate of another issue"
gh label create "wont-fix" --color "ffffff" --description "This will not be worked on"
gh label create "breaking-change" --color "d73a4a" --description "Contains breaking changes"
gh label create "security" --color "d73a4a" --description "Security-related issue"
```