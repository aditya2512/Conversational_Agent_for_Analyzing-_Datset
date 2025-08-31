# Conversational Data Explorer

An intelligent chatbot that enables data analysis and visualization through natural language conversations. Built with LangChain, LangGraph, and OpenAI's GPT models.

## Project Overview

This project implements a multi-turn conversational agent for data exploration, showcasing:

### Functionality 
- Multi-turn conversation support with context retention
- Integrated tools for data loading, analysis, and visualization
- LangGraph-based state management and workflow
- Error handling and graceful fallbacks
- Type-safe tool implementations with Pydantic validation

### Reasoning Flow 
- Clear decision-making process in tool selection
- Context-aware response generation
- Structured conversation management
- Intuitive command parsing and execution
- Natural language understanding for data queries

### Modularity 
- Clean separation of concerns:
  - Tool definitions (Load, Analyze, Plot)
  - State management
  - Conversation flow
  - Error handling
- Reusable components and extensible architecture

### Creativity 
- Intuitive natural language interface
- Flexible data analysis capabilities
- Interactive visualization options
- User-friendly error messages
- Polished chat experience

### Documentation
- Comprehensive setup instructions
- Clear code documentation
- Detailed usage examples
- Demonstration interactions
- Architecture explanation

## Features

- **Data Loading**: Load and manage CSV files seamlessly
- **Smart Analysis**: Execute pandas operations through natural language
- **Interactive Visualization**: Create line, bar, and scatter plots easily
- **Continuous Conversations**: Maintains context across multiple interactions
- **Error Resilience**: Robust error handling and validation
- **Type Safety**: Fully typed with Pydantic models
- **Modern Architecture**: Built on LangGraph for reliable conversation flow

## Requirements and Installation

### Prerequisites
- Python 3.8+
- OpenAI API key

### Dependencies
```bash
pip install langchain langchain-openai langgraph pandas matplotlib
```

### Setup
1. Clone the repository
2. Install dependencies
3. Set your OpenAI API key:
```python
os.environ["OPENAI_API_KEY"] = "your-api-key-here"
```

## Architecture

### Core Components

1. **Tools**
   - `LoadDataTool`: CSV file management with Pydantic validation
   - `AnalyzeDataTool`: Data analysis with safe query execution
   - `PlotDataTool`: Matplotlib-based visualization with error handling

2. **State Management**
   - `AgentState`: TypedDict for conversation tracking
   - Message history management
   - Tool state persistence

3. **Conversation Flow**
   - LangGraph-based state machine
   - OpenAI tools agent integration
   - Continuous chat loop with graceful exit

## Usage Examples

### 1. Data Loading
```
Human: Load sample.csv
Assistant: Let me help you load that CSV file.
Loaded 6 rows x 3 columns from sample.csv.
```

### 2. Data Analysis
Available commands:
- `head(n)`: Show first n rows
- `describe()`: Statistical summary
- `columns`: List column names
- `value_counts(col)`: Frequency count for a column
- `top_by(col, n)`: Top n rows sorted by column

Example:
```
Human: Show me a summary of the data
Assistant: Here's the statistical summary:
             month  revenue    units
count          6.0    6.000    6.000
mean           NaN 1516.667  145.000
std            NaN  420.317   35.468
min            NaN  900.000   90.000
25%            NaN 1275.000  125.000
50%            NaN 1550.000  145.000
75%            NaN 1750.000  170.000
max            NaN 2100.000  195.000
```

### 3. Data Visualization
Supported plot types:
- Line plots: `plot_type, x_col, y_col, title`
- Bar plots: `plot_type, x_col, y_col, title`
- Scatter plots: `plot_type, x_col, y_col, title`

Example:
```
Human: Create a line plot of revenue over months
Assistant: Creating a line plot with months on x-axis and revenue on y-axis.
Plot created.
```

## Exit Commands
To exit the conversation, use any of these commands:
- quit
- exit
- q

The chatbot will gracefully end the conversation and save any work done during the session.

## Error Handling
The system provides clear error messages for:
- Missing or invalid files
- Incorrect column names
- Invalid analysis commands
- Plot generation errors
- API issues

Each error includes actionable feedback to help resolve the issue.

2. **Analysis Operations**
```python
"head(5)"                     # First 5 rows
"describe()"                  # Statistical summary
"columns"                     # List columns
"value_counts(category)"      # Count by category
"top_by(revenue, 10)"        # Top 10 by revenue
```

3. **Visualization Commands**
```python
"line, date, revenue, Sales Trend"
"bar, category, units, Units by Category"
"scatter, price, sales, Price vs Sales"
```

### Example Conversation

```python
You: Load sample.csv
Assistant: Loaded 6 rows x 3 columns from sample.csv.

You: describe()
Assistant: Here's the data summary:
              revenue        units
count     6.000000     6.000000
mean   1516.666667   145.000000
std     424.311523    38.781329
min     900.000000    90.000000
25%    1275.000000   122.500000
50%    1550.000000   145.000000
75%    1750.000000   170.000000
max    2100.000000   195.000000

You: bar, month, revenue, Monthly Revenue
Assistant: Plot created.
```

## Advanced Features

1. **Type Safety**
   - Pydantic models for all tools
   - Runtime type checking
   - Schema validation

2. **Error Handling**
   - Graceful file loading errors
   - Safe query execution
   - Input validation
   - User-friendly error messages

3. **Extensibility**
   - Easy to add new tools
   - Customizable visualizations
   - Configurable chat behavior

## Project Structure

```
conversational_data_explorer/
│
├── conversational_agent_refactored_v4.ipynb    # Main implementation
│
│
├── sample.csv         # Simple demo dataset
├── sample_sales.csv    # Complex demo dataset
│
└── README.md          # Project documentation
```

## Implementation Details

### Tools
1. **LoadDataTool**
   - CSV file loading
   - DataFrame management
   - Error handling for file operations

2. **AnalyzeDataTool**
   - Data analysis operations
   - Statistical computations
   - Query parsing and execution

3. **PlotDataTool**
   - Visualization generation
   - Multiple plot types
   - Customizable chart attributes

### State Management
- `AgentState`: TypedDict for message tracking
- `ConversationState`: Context maintenance
- LangGraph for workflow control

### Conversation Flow
1. User Input → Message Processing
2. Tool Selection → Execution
3. Response Generation → Output Formatting
4. Context Update → State Maintenance

## Development Time

- **Estimated Time**: 6-10 hours
- **Breakdown**:
  - Initial Setup: 1 hour
  - Core Implementation: 3-4 hours
  - Testing & Refinement: 1-2 hours
  - Documentation: 1-2 hours



## Example Outputs

Here are some example interactions using both sample datasets:

### Using sample.csv (Simple Dataset)
```
You: Load sample.csv
Assistant: Loaded 6 rows x 3 columns from sample.csv.

You: describe()
Assistant: Here's the data summary:
              revenue        units
count     6.000000     6.000000
mean   1516.666667   145.000000
std     424.311523    38.781329
min     900.000000    90.000000
25%    1275.000000   122.500000
50%    1550.000000   145.000000
75%    1750.000000   170.000000
max    2100.000000   195.000000

You: line, month, revenue, Monthly Revenue Trend
Assistant: Plot created. [Shows line plot of revenue over months]
```

### Using sample_sales.csv (Complex Dataset)
```
You: Load sample_sales.csv
Assistant: Loaded 10 rows x 5 columns from sample_sales.csv.

You: columns
Assistant: date, product, category, quantity, revenue

You: value_counts(category)
Assistant: Electronics    5
Furniture     5
Name: category, dtype: int64

You: top_by(revenue, 3)
Assistant: date         product    category  quantity  revenue
2024-01-04  Phone    Electronics       15     7500
2024-01-03  Laptop   Electronics        7     7000
2024-01-05  Laptop   Electronics        6     6000

You: bar, product, revenue, Product Revenue Analysis
Assistant: Plot created. [Shows bar chart comparing product revenues]

You: What's the total revenue by category?
Assistant: Using the analyze_data tool to calculate total revenue by category:
category
Electronics    30500
Furniture       7100
Name: revenue, dtype: int64
```

The example outputs demonstrate:
1. Basic data loading and inspection
2. Statistical analysis
3. Value counting and aggregation
4. Top-N analysis
5. Data visualization
6. Natural language queries

Both datasets showcase different aspects of the agent's capabilities:
- `sample.csv`: Simple time-series data with revenue trends
- `sample_sales.csv`: Complex sales data with multiple dimensions for analysis

