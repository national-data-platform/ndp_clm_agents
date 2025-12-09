# CLM Agents in NDP

AI-powered agents for querying and analyzing California Landscape Metrics (CLM) datasets using natural language. Built with Pydantic AI and FastMCP.

## Overview

This repository provides three Jupyter notebooks demonstrating different capabilities for interacting with CLM datasets:

1. **Simple Agent** - Basic dataset search with conversation history
2. **Agent with Logfire** - Enhanced logging and observability
3. **Enhanced Agent** - Full-featured analysis with maps and visualizations

## Features

- 🔍 **Natural Language Search** - Find datasets using plain English queries
- 💬 **Conversational Interface** - Maintains context across questions
- 📊 **Statistical Analysis** - Compute zonal statistics for California counties
- 🗺️ **Interactive Maps** - Visualize datasets with WMS layers
- 📈 **Distribution Charts** - Compare data distributions across regions
- 🔬 **Threshold Analysis** - Calculate areas above/below specified thresholds
- 📝 **Observability** - Optional Logfire integration for debugging

## Prerequisites

- Python 3.10 or higher
- Jupyter Notebook or JupyterLab
- OpenAI API key (or NRP API key for Qwen3 model)

## Installation

1. Clone the repository:
```bash
git clone https://github.com/yourusername/clm-agents-ndp.git
cd clm-agents-ndp
```

2. Install dependencies:
```bash
pip install -r requirements.txt
```

3. Create a `.env` file with your API key:
```bash
# For OpenAI
OPENAI_API_KEY=your_openai_api_key

# Or for NRP (optional)
NRP_API_KEY=your_nrp_api_key
```

## Quick Start

### Simple Agent (Recommended for beginners)

Open `simple_clm_agent.ipynb` and run all cells. This provides a basic chat interface for dataset search.

**Example questions:**
- "Find datasets about carbon turnover"
- "What are the units for this dataset?"
- "Search for burn probability datasets"

### Enhanced Agent (Full features)

Open `enhanced_clm_agent.ipynb` for advanced capabilities including maps and visualizations.

**Example questions:**
- "What is the average carbon turnover time in Los Angeles?"
- "Show me a map of the annual burn probability dataset"
- "Compare the distribution of carbon turnover between San Diego and Orange county"
- "Which county has the highest mean carbon turnover time?"

### Agent with Logfire (For debugging)

For observability and debugging, use `simple_clm_agent_with_logfire.ipynb`:

1. First authenticate with Logfire:
```bash
logfire auth
```

2. Run the notebook to see detailed logs at https://logfire.pydantic.dev

## Notebooks

### 1. simple_clm_agent.ipynb

Basic agent demonstrating core functionality:
- Dataset search using semantic similarity
- Conversation history management
- Simple chat interface
- Support for OpenAI GPT-4o-mini or NRP Qwen3

**Best for:** Learning the basics, simple queries

### 2. simple_clm_agent_with_logfire.ipynb

Same as the simple agent but with comprehensive logging:
- All API calls logged to Logfire cloud
- Performance metrics tracking
- Error tracking and debugging
- HTTP request monitoring

**Best for:** Development, debugging, understanding agent behavior

### 3. enhanced_clm_agent.ipynb

Full-featured agent with advanced capabilities:
- Statistical analysis (mean, median, min, max, std)
- Threshold-based area calculations
- Interactive WMS map visualization
- Distribution charts and histograms
- Multi-county comparisons
- Ranking and filtering

**Best for:** Production use, complex analysis tasks

## Architecture

```
User Question
     ↓
ConversationalAgent (manages history)
     ↓
Pydantic AI Agent (processes with LLM)
     ↓
Tools (search_datasets, compute_stats, etc.)
     ↓
FastMCP Client → CLM-MCP Server
     ↓
GeoServer (WCS/WFS) → Datasets
     ↓
Response (with data/maps/charts)
```

## Available Tools

The enhanced agent includes these tools:

- `search_and_select_dataset` - Find relevant datasets by topic
- `get_county_statistics` - Compute zonal statistics
- `get_area_above_threshold` - Calculate area above a threshold
- `get_area_below_threshold` - Calculate area below a threshold
- `show_map` - Display interactive WMS map
- `get_value_distribution` - Get data distribution for charts

## Model Options

### OpenAI GPT-4o-mini (Default)
- Fast and reliable
- 60 second default timeout
- Requires OpenAI API key

### NRP Qwen3 (Alternative)
- Open-source model
- 180 second default timeout
- Requires NRP API key
- Set `MODEL = "nrp"` in the configuration cell

## Example Queries

### Basic Search
```
"Find datasets about carbon turnover"
"What datasets are available for burn probability?"
```

### Statistical Analysis
```
"What is the average carbon turnover time in Los Angeles?"
"Find the maximum annual burn probability in San Diego county"
"Rank the top 5 counties by mean carbon turnover time"
```

### Threshold Analysis
```
"What percentage of San Diego County has carbon turnover time above 100 years?"
"Show all counties where at least 30% of area has carbon turnover less than 20 years"
```

### Visualization
```
"Show me a map of the carbon turnover dataset"
"Show the data distribution for San Diego and Los Angeles"
"Compare distributions between San Diego, Los Angeles, and Orange county"
```

### Follow-up Questions
```
User: "What is the average carbon turnover in Los Angeles?"
Agent: [provides answer]
User: "How about San Diego?"
Agent: [understands context and provides San Diego statistics]
```

## Configuration

The notebooks connect to:
- **MCP Server**: `https://wenokn.fastmcp.app/mcp`
- **GeoServer**: `https://sparcal.sdsc.edu/geoserver`

These are configured in the `BASE_CONFIG` dictionary and can be modified if needed.

## Troubleshooting

### Timeout Errors
- For complex queries, the agent may timeout
- Try breaking down the question into simpler parts
- Switch to OpenAI model if using NRP
- Increase timeout in `conv_agent.ask(question, timeout=300)`

### Map Not Displaying
- Ensure the dataset has been selected via search first
- Check that WMS URLs are accessible
- Verify internet connection

### Chart Not Showing
- Distribution charts require multiple data points
- Ensure you're querying counties that exist in the dataset
- Check that the distribution tool received data

## Contributing

Contributions are welcome! Please feel free to submit issues or pull requests.

## License

This project is licensed under the MIT License - see the LICENSE file for details.

## Acknowledgments

- Built with [Pydantic AI](https://ai.pydantic.dev/)
- Uses [FastMCP](https://github.com/jlowin/fastmcp) for Model Context Protocol
- California Landscape Metrics data from SDSC
- Powered by OpenAI GPT-4o-mini or NRP Qwen3

## Support

For issues or questions:
- Open an issue on GitHub
- Check existing issues for solutions
- Review the example questions in each notebook

## Citation

If you use this work in your research, please cite:

```bibtex
@software{clm_agents_ndp,
  title = {CLM Agents in NDP: AI-powered California Landscape Metrics Analysis},
  year = {2024},
  license = {MIT}
}
```
