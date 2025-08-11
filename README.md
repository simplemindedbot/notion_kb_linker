# Notion Knowledge Base Auto-Linker

An intelligent automation tool that analyzes your Notion knowledge base to automatically generate relevant tags and create semantic cross-links between pages, transforming a collection of isolated notes into a highly interconnected knowledge graph.

## 🎯 What It Does

- **Automatic Tagging**: Analyzes page content to suggest and apply relevant tags
- **Smart Cross-Linking**: Identifies semantically similar pages and creates bidirectional links
- **Content Discovery**: Helps surface related information you might have forgotten existed
- **Knowledge Graph Enhancement**: Transforms isolated pages into an interconnected web of knowledge

## 🧠 How It Works

### Semantic Analysis
- Uses advanced NLP and sentence transformers to understand page content
- Calculates semantic similarity between all pages in your database
- Identifies themes, topics, and relationships automatically

### Intelligent Linking
- Finds pages that should reference each other based on content similarity
- Creates contextually appropriate cross-links within page content
- Maintains bidirectional relationships for better knowledge discovery

### Safe Automation
- **Dry-run mode**: Preview all changes before applying them
- **Backup system**: Complete database export before making any modifications
- **Approval workflows**: Choose your comfort level from per-change to batch approval
- **Rollback capability**: Undo changes if needed

## 🚀 Quick Start

### Prerequisites
- Python 3.8+
- Notion workspace with API access
- A Notion database to analyze (your "Knowledgebase")

### Installation
```bash
git clone https://github.com/yourusername/notion_kb_linker.git
cd notion_kb_linker
pip install -r requirements.txt
```

### Configuration
1. Create a Notion integration at [notion.so/my-integrations](https://notion.so/my-integrations)
2. Share your Knowledgebase database with the integration
3. Set environment variables:
```bash
export NOTION_TOKEN="secret_xxxxxxxxxxxx"
export NOTION_DATABASE_ID="your-database-id"
```

### First Run
```bash
# Always start with a backup and dry run
python notion_linker.py --backup --dry-run --report

# Review the generated report, then run with approval required
python notion_linker.py --backup --initial-run --require-approval
```

## 📋 Usage Modes

### Safety-First Approach
```bash
# Create backup and preview changes (no modifications)
python notion_linker.py --backup --dry-run --report

# First run with manual approval for each change
python notion_linker.py --initial-run --require-approval
```

### Approval Modes
```bash
# Review and approve each suggested link/tag individually
python notion_linker.py --mode=per-change

# Review all changes for each page as a bundle
python notion_linker.py --mode=per-page

# Review summary and approve all changes at once
python notion_linker.py --mode=batch

# Fully automated (use after establishing trust)
python notion_linker.py --auto
```

## ⚙️ Configuration Options

### Environment Variables
- `NOTION_TOKEN`: Your Notion integration token
- `NOTION_DATABASE_ID`: Target database ID to analyze
- `SIMILARITY_THRESHOLD`: Minimum similarity score for link suggestions (0.0-1.0)
- `MAX_LINKS_PER_PAGE`: Maximum cross-links to add per page
- `TAG_CONFIDENCE_THRESHOLD`: Minimum confidence for tag suggestions

### Customizable Parameters
- **Similarity thresholds**: Control how related pages need to be for linking
- **Link placement**: Choose between inline mentions or dedicated "Related Pages" sections
- **Tag strategies**: Use NLP keyword extraction or LLM-based tag generation
- **Backup retention**: How long to keep backup files

## 🛡️ Safety Features

### Comprehensive Backups
- Full database export with all content and metadata
- Timestamped backups with change logs
- Selective or complete restoration capability

### Multiple Approval Levels
- **Dry Run**: See all proposed changes without making any modifications
- **Interactive Preview**: View exactly where links will be inserted
- **Confidence Scores**: Each suggestion includes a confidence rating
- **Change Tracking**: Log of all modifications with ability to selectively undo

### Smart Preservation
- Existing manual links and tags are preserved
- Formatting and page structure maintained
- User modifications protected during subsequent runs

## 🔧 Technical Architecture

**Built With:**
- `notion-client`: Official Notion API integration
- `sentence-transformers`: Semantic similarity analysis
- `scikit-learn`: Machine learning for clustering and similarity
- `spacy`: Natural language processing
- `click`: Command-line interface
- `rich`: Beautiful terminal output

**Core Process:**
1. **Extract**: Read all pages and content from your Notion database
2. **Analyze**: Generate semantic embeddings and calculate similarity scores
3. **Recommend**: Identify high-confidence tagging and linking opportunities
4. **Preview**: Generate detailed reports of proposed changes
5. **Apply**: Implement approved changes with full tracking and rollback capability

## 📊 What You'll See

### Before
- Isolated pages with few or generic tags
- Manual effort required to find related content
- Knowledge buried in unconnected notes

### After
- Rich tag taxonomy reflecting your actual content themes
- Smart cross-links connecting related concepts
- Easy discovery of forgotten but relevant information
- Self-maintaining knowledge graph that grows with your content

## 🤝 Contributing

Contributions welcome! This tool is designed to be:
- **Safe**: Multiple safeguards prevent data loss
- **Transparent**: Clear reporting of all changes
- **Flexible**: Adaptable to different knowledge management styles
- **Extensible**: Easy to add new analysis techniques

## 📄 License

MIT License - see LICENSE file for details

## 🆘 Support

- Check the generated reports for insights into what changes are proposed
- Start with dry-run mode to build confidence in the tool
- Use per-change approval mode initially to understand the tool's logic
- Review the backup files location for emergency restoration

---

Transform your Notion workspace from a collection of notes into an intelligent, interconnected knowledge system that helps you rediscover and connect your ideas.
