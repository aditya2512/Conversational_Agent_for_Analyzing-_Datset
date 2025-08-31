# Conversational Data Explorer

An intelligent chatbot that enables data analysis and visualization through natural language conversations. Built with LangChain, LangGraph, and OpenAI's GPT models.

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

## Usage Guide

### Data Analysis Commands

1. **Loading Data**
```python
"Load sample.csv"
```

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

## Contributing

1. Fork the repository
2. Create a feature branch
3. Submit a pull request

## License

MIT License

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
Assistant: Electronics    6
Furniture     4
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
