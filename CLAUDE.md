# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

# Notion Knowledge Base Auto-Linker - Development Guide

## Project Overview

This tool automatically analyzes a Notion Knowledge Base database to:
1. **Generate relevant tags** for pages based on content analysis
2. **Create cross-links** between semantically similar pages
3. **Enhance knowledge discovery** through improved interconnections

## Technical Architecture

### Core Components

**1. Notion API Integration**
- Use `notion-client` library for official API access
- Read all pages from specified Knowledgebase database
- Handle different Notion block types (text, headings, lists, callouts, etc.)
- Write back tags and content modifications

**2. Content Analysis Engine**
- **Text Processing**: Clean and normalize page content from Notion blocks
- **Embedding Generation**: Use `sentence-transformers` for semantic embeddings of page content
- **Similarity Calculation**: Cosine similarity between page embeddings to find related content
- **Tag Extraction**: NLP-based keyword extraction or OpenAI API for intelligent tag generation

**3. Link Recommendation System**
- Calculate semantic similarity matrix between all pages
- Identify high-confidence cross-linking opportunities
- Generate bidirectional link suggestions
- Preserve existing manual links and tags

### Required Dependencies

```python
notion-client          # Official Notion API wrapper
sentence-transformers  # For semantic embeddings (e.g., 'all-MiniLM-L6-v2')
scikit-learn          # For similarity calculations and clustering
spacy                 # For text processing and NLP
openai                # Optional: for enhanced tag generation
click                 # For command-line interface
rich                  # For beautiful CLI output and progress bars
json                  # For backup/restore functionality
```

## Development Commands

This project is in early development. The main application will be `notion_linker.py` when implemented.

### Primary Commands
```bash
# Development and testing (when implemented)
python -m pytest                             # Run tests
python notion_linker.py --help              # View available options

# Main application usage patterns
python notion_linker.py --backup --dry-run --report         # Safe preview mode
python notion_linker.py --initial-run --require-approval    # First run with approval
python notion_linker.py --mode=per-change                   # Interactive approval mode
python notion_linker.py --auto                              # Automated mode
```

### Environment Setup
```bash
# Required environment variables
export NOTION_TOKEN="secret_xxxxxxxxxxxx"     # Notion integration token  
export NOTION_DATABASE_ID="your-database-id"  # Target database ID
export SIMILARITY_THRESHOLD=0.7               # Link similarity threshold (0.0-1.0)
export MAX_LINKS_PER_PAGE=10                  # Maximum cross-links per page
export TAG_CONFIDENCE_THRESHOLD=0.6           # Tag generation confidence threshold
```

## Key Architecture Patterns

### Multi-Phase Processing Pipeline
The application follows a structured 4-phase approach:
1. **Data Extraction**: Notion API integration with comprehensive block type handling
2. **Content Analysis**: Semantic embedding generation using sentence-transformers  
3. **Recommendation Generation**: Similarity-based cross-linking with confidence scoring
4. **Safe Application**: Backup-first approach with multiple approval workflows

### Safety-First Design Philosophy  
- **Always backup before modifications**: Complete database export with metadata
- **Dry-run everything first**: Generate reports without Notion API writes
- **Multiple approval levels**: From per-change to batch approval modes
- **Full rollback capability**: Track and selectively undo any changes
- **Preserve existing content**: Maintain user manual links and tags

### Core Technical Components

**Notion API Integration** (`notion-client` library)
- Handle all Notion block types (text, headings, lists, callouts, etc.)
- Implement proper rate limiting with exponential backoff
- Preserve page structure and formatting during modifications

**Semantic Analysis Engine**
- Use `sentence-transformers` (e.g., 'all-MiniLM-L6-v2') for embeddings
- Calculate cosine similarity matrices between all pages
- Support both NLP keyword extraction and OpenAI-based tag generation

**CLI Interface** (using `click` and `rich`)
- Rich progress bars and interactive previews
- Multiple approval workflow modes
- Beautiful terminal output with confidence scores

## Safety Framework

**1. Baseline Backup System**
- Export complete database to timestamped JSON before any changes
- Include all page content, properties, relationships, and metadata
- Store locally with optional cloud backup integration
- Enable full or selective restoration

**2. Dry Run Mode**
- Analyze content and generate all recommendations
- Create detailed report without making any Notion API writes
- Show before/after previews of proposed changes
- Generate confidence scores for all suggestions

**3. Approval Workflows**
- **Per-change**: Review each tag/link suggestion individually with context
- **Per-page**: Review all proposed changes for a single page as bundle
- **Batch**: Review summary statistics and approve all changes
- **Interactive preview**: Show exact placement of proposed links in content

**4. Change Tracking & Rollback**
- Log all applied changes with timestamps and confidence scores
- Track auto-generated vs manually created content
- Enable selective undo of specific changes or full rollback
- Preserve user manual modifications during subsequent runs

## Implementation Workflow

### Phase 1: Data Extraction
1. Authenticate with Notion API using integration token
2. Query specified database to get all pages
3. Extract content from all block types while preserving structure
4. Parse existing tags and manual links to preserve them

### Phase 2: Content Analysis
1. Clean and preprocess text content from pages
2. Generate semantic embeddings for each page using sentence transformers
3. Calculate similarity matrix between all page pairs
4. Extract potential tags using NLP techniques or LLM analysis

### Phase 3: Recommendation Generation
1. Identify pages with high semantic similarity (configurable threshold)
2. Generate cross-link suggestions with confidence scores
3. Propose relevant tags based on content analysis
4. Create bidirectional linking recommendations

### Phase 4: Output Generation
1. **Dry Run**: Generate detailed HTML/markdown report of all proposed changes
2. **Backup**: Create complete database export with timestamp
3. **Interactive Approval**: Present changes based on selected approval mode
4. **Application**: Apply approved changes via Notion API with error handling

## Development Implementation Notes

### Current Status
This is a greenfield project - the main implementation files do not exist yet. When developing:

1. **Start with MVP approach**: Basic content extraction → similarity calculation → dry-run reporting
2. **Implement safety-first**: All operations must have backup and dry-run capabilities
3. **Follow the 4-phase pipeline**: Data extraction → analysis → recommendations → safe application

### Critical Error Handling Requirements
- **Notion API rate limits**: Implement exponential backoff for all API calls
- **Graceful degradation**: Handle pages with minimal content or unusual structures
- **Formatting preservation**: Maintain exact formatting when inserting links
- **Circular link detection**: Prevent infinite linking loops
- **Schema change resilience**: Handle database structure changes between runs

### Key Configuration Points
All thresholds and limits should be configurable via environment variables:
- Similarity thresholds for cross-link generation (default: 0.7)
- Maximum links per page to prevent clutter (default: 10)  
- Tag confidence thresholds (default: 0.6)
- Link placement strategy (inline vs dedicated sections)
- Backup retention policies for cleanup

### Success Metrics to Track
- Orphaned page reduction (pages with no incoming links)
- Tag taxonomy coherence and coverage
- Cross-link network density and quality
- Processing efficiency for large knowledge bases

The goal is transforming loosely connected Notion databases into highly interconnected knowledge graphs that enhance discoverability and maintain themselves over time.

---

## Project Development Status & Progress

### Completed Milestones

**✅ Project Foundation (Phase 0)**
- [x] **Repository Setup**: Initialized GitHub repository with proper structure
- [x] **Environment Configuration**: Set up Python virtual environment with core dependencies
- [x] **Security Framework**: Implemented comprehensive .gitignore with project-specific exclusions
- [x] **Documentation Structure**: Created comprehensive project documentation and requirements

**✅ Development Team Assembly (Phase 0.5)**
- [x] **Specialized Agent Team**: Created minimal but comprehensive development team with 3 specialized Claude Code agents:
  - **notion-api-safety-engineer**: Notion API integration, backup systems, safety protocols
  - **semantic-analysis-engineer**: NLP processing, embeddings, similarity calculations
  - **cli-workflow-designer**: User interfaces, approval workflows, configuration management
- [x] **Project Coordination**: notion-nlp-specialist for overall project guidance
- [x] **Requirements Analysis**: product-requirements-architect for feature planning

**✅ Project Infrastructure (Phase 0.5)**
- [x] **GitHub Integration**: Complete issue templates, labels, and milestone structure
- [x] **Development Workflow**: Proper branching strategy and development practices
- [x] **Security Audit**: Repository scan for secrets, secure environment variable handling
- [x] **IDE Configuration**: Removed accidentally committed IDE files (.idea/) from repository

### Current Project State

**📁 Repository Structure**
```
notion_kb_linker/
├── .claude/
│   ├── agents/                    # Specialized development agents
│   └── settings.local.json        # Claude Code configuration
├── .github/
│   ├── ISSUE_TEMPLATE/           # GitHub issue templates
│   ├── LABELS.md                 # Project labels
│   └── MILESTONES.md            # Development milestones
├── docs/
│   ├── requirements.md           # Comprehensive technical requirements
│   ├── product-backlog.md       # User stories and features
│   └── github-setup-guide.md    # Development workflow guide
├── venv/                        # Python virtual environment
├── .env.example                 # Environment variable template
├── .gitignore                   # Comprehensive exclusions
├── CLAUDE.md                    # This development guide
├── README.md                    # Project overview
└── requirements.txt             # Python dependencies
```

**🔧 Environment Setup**
- Python 3.10+ virtual environment activated
- Core dependencies installed: sentence-transformers, scikit-learn, spacy, notion-client, click, rich
- Environment variables configured via .env.example template
- Security measures in place to prevent credential exposure

**📋 Next Development Phase: MVP Implementation**

The project is now ready for core implementation. The next major milestone is **Phase 1: MVP Development** which includes:

1. **Core Application Structure**
   - [ ] Create main `notion_linker.py` application entry point
   - [ ] Implement configuration management system
   - [ ] Set up logging and error handling framework

2. **Notion API Integration (notion-api-safety-engineer)**
   - [ ] Implement Notion client authentication
   - [ ] Create database query and page extraction functionality
   - [ ] Build backup system with timestamped exports
   - [ ] Implement rate limiting with exponential backoff

3. **Content Analysis Engine (semantic-analysis-engineer)**
   - [ ] Text preprocessing pipeline for Notion content
   - [ ] Semantic embedding generation using sentence-transformers
   - [ ] Similarity matrix calculations between pages
   - [ ] Tag extraction and recommendation algorithms

4. **CLI Interface (cli-workflow-designer)**
   - [ ] Command-line interface with multiple operation modes
   - [ ] Dry-run reporting with detailed change previews
   - [ ] Interactive approval workflows (per-change, per-page, batch)
   - [ ] Progress bars and rich terminal output

**🎯 Development Priorities**
1. **Safety First**: All features must implement backup and dry-run capabilities
2. **Incremental Development**: Start with basic content extraction and similarity calculation
3. **Testing Framework**: Implement comprehensive testing for each component
4. **Documentation**: Maintain up-to-date documentation as features are developed

### Virtual Environment Information

**Current Environment**: `venv/` (Python 3.10+)

**Activation Command**: 
```bash
# Stored in CLAUDE.md for future reference
source venv/bin/activate  # macOS/Linux
# venv\Scripts\activate   # Windows
```

**Dependencies Installed**:
- sentence-transformers==2.2.2 (semantic embeddings)
- scikit-learn (similarity calculations)
- spacy (text processing)
- notion-client (official Notion API)
- click (CLI framework)
- rich (terminal formatting)

### Security & Best Practices

**✅ Security Measures Implemented**
- Comprehensive .gitignore preventing credential exposure
- Environment variable template (.env.example) for secure configuration
- Repository audit completed - no secrets committed
- IDE-specific files properly excluded

**⚠️ Security Reminders**
- Always use .env.example as template, never commit actual .env files
- API tokens and database IDs must remain in environment variables
- Regular security audits before pushing code
- Backup files should be excluded from repository

### Development Workflow

**Branch Strategy**: 
- `main` branch for stable releases
- Feature branches for development work
- Working branch creation before each sprint

**Commit Standards**:
- Descriptive commit messages following conventional commit format
- Security-focused commits when handling sensitive configurations
- Claude Code attribution in commit messages

The project foundation is now complete and ready for core feature implementation. The specialized agent team is configured and prepared to tackle their respective domains in the upcoming development phases.
