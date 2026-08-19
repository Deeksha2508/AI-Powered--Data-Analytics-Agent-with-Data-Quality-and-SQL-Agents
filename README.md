
# AI-Powered Data Analytics Agent

An agentic AI pipeline built in Python that automates the end-to-end data analytics workflow — from data ingestion and cleaning to SQL querying, visualization, and AI-generated business insights — powered by **Google Gemini 2.5 Flash**.

This project implements a multi-agent architecture where each agent handles a distinct stage of the analytics pipeline. Instead of one monolithic analysis script, every responsibility is encapsulated in its own agent class, keeping the system modular, extensible, and easy to debug.

---

## 1. Overview

| | |
|---|---|
| **Type** | Multi-agent AI analytics pipeline |
| **Built for** | Structured CSV data (tested on the Superstore Sales Dataset) |
| **Core AI Model** | Google Gemini 2.5 Flash |
| **Environment** | Google Colab / Python 3 |
| **Author** | Deeksha — B.Tech ECE, Thapar Institute of Engineering and Technology |

---

## 2. Description

- **8 specialized agents**, each independently testable, covering ingestion → cleaning → quality scoring → analytics → SQL → visualization → AI insights → natural-language Q&A
- **Dataset used for testing:** Sample Superstore dataset (order-level retail records — Sales, Profit, Category, Region, Product Name)
- **AI Model:** Google Gemini 2.5 Flash (`google-generativeai`)
- **Data Quality Score:** automatically computed as the percentage of non-missing cells across the dataset
- **Natural language Q&A:** users can ask plain-English questions about the data and get an answer, no SQL required
- **Roadmap:** extending the pipeline to work with more dataset types beyond retail/sales data

---

## 3. Input / Output

The table below shows the kind of plain-English question a user can type, which agent handles it, and what comes back:

| # | User Question (Input) | Agent Used | Output |
|---|---|---|---|
| 1 | "What's our total profit this year?" | `QueryAgent` | Direct numeric answer generated from the dataframe |
| 2 | "Which region has the highest profit margin?" | `QueryAgent` | Natural-language answer with the top region named |
| 3 | "Show me sales by category" | `SQLAgent` | Auto-generated SQL run on the dataframe via `pandasql`, returned as a table |
| 4 | "What are our top 10 products by sales?" | `AnalyticsAgent` | Ranked product-level revenue breakdown |
| 5 | "Summarize the business risks and opportunities" | `InsightAgent` | Gemini-generated report: key insights, risks, growth opportunities, recommendations |
| 6 | "How clean is this dataset?" | `DataQualityAgent` | Data quality report + quality score (%) |

Every row above runs through the same pipeline: **question → relevant agent → Gemini reasoning (where needed) → plain-English or visual answer.**

---

## 4. Live Demo

**Try it here → [Ask the Data Analytics Agent](https://deeksha2508.github.io/ai-data-analytics-agent/demo.html)**

Click the link, type a question like *"which region has the highest sales?"* or pick one of the suggested prompts, and see how the agent would respond — no setup required.

> Note: this hosted demo is a lightweight front-end simulation of the agent's natural-language Q&A step, built so visitors can interact with the concept directly from GitHub without running the notebook. The full pipeline (real Gemini calls + your own data) runs in Google Colab — see [Setup & Installation](#setup--installation) below.

---

## 5. Screenshot of the Interface

> Add screenshots or a short GIF of your Colab output here so visitors can see it without running the notebook — e.g.:
> - The data quality report output
> - The Sales-by-Region bar chart and Category pie chart (Plotly)
> - A sample `query_agent.answer_question(...)` call and its printed answer
> - The Gemini-generated business insights report

```
![Data Quality Report](assets/quality_report.png)
![Sales by Region](assets/sales_by_region.png)
![Sample Q&A](assets/sample_query.png)
```

---

## Agent Architecture

| Agent | Responsibility |
|---|---|
| `DataIngestionAgent` | Loads CSV data with encoding support |
| `DataCleaningAgent` | Removes duplicates and null values |
| `DataQualityAgent` | Generates a data quality report and computes a quality score |
| `AnalyticsAgent` | Computes KPIs — total sales, profit, top products, top regions |
| `SQLAgent` | Runs SQL queries on the dataframe using `pandasql` |
| `VisualizationAgent` | Creates interactive Plotly charts (bar, pie) |
| `InsightAgent` | Calls the Gemini API to generate business insights from the data summary |
| `QueryAgent` | Answers natural language questions about the dataset using Gemini |

## Tech Stack

- **Language:** Python 3
- **Environment:** Google Colab
- **AI Model:** Google Gemini 2.5 Flash (`google-generativeai`)
- **Data Processing:** Pandas, NumPy
- **SQL on DataFrames:** pandasql
- **Visualization:** Plotly Express
- **File Handling:** openpyxl

## Setup & Installation

### 1. Clone the repository
```bash
git clone https://github.com/Deeksha2508/ai-data-analytics-agent.git
cd ai-data-analytics-agent
```

### 2. Install dependencies
```bash
pip install google-generativeai plotly pandas openpyxl pandasql
```

### 3. Add your Gemini API Key
In the notebook, replace the placeholder with your key:
```python
GOOGLE_API_KEY = "YOUR_GEMINI_API_KEY"
```
Get a free API key at [Google AI Studio](https://aistudio.google.com/).

### 4. Upload your dataset
Place `Superstore.csv` in your working directory, or upload it via Colab's file upload cell.

## Pipeline Walkthrough

**Phase 1 — Data Ingestion & Cleaning**
```python
df = ingestion_agent.load_data("Superstore.csv")
df = cleaning_agent.clean(df)
```

**Phase 2 — Data Quality Report**
```python
quality_report = quality_agent.generate_report(df)
# Outputs: missing values, duplicate rows, data types, quality score (%)
```

**Phase 3 — Analytics**
```python
analytics_agent.total_sales(df)
analytics_agent.total_profit(df)
analytics_agent.top_products(df)
```

**Phase 4 — SQL Queries**
```python
query = """
SELECT Category, SUM(Sales) as TotalSales
FROM df
GROUP BY Category
ORDER BY TotalSales DESC
"""
sql_agent.execute_query(query, df)
```

**Phase 5 — Visualization**
```python
visualization_agent.sales_by_region(df)   # Bar chart
visualization_agent.category_sales(df)    # Pie chart
```

**Phase 6 — AI Insights (Gemini)**
```python
insights = insight_agent.generate_insights(df)
print(insights)
# Returns: key insights, business risks, growth opportunities, recommendations
```

**Phase 7 — Natural Language Querying**
```python
answer = query_agent.answer_question(df, "Which region has the highest profit margin?")
print(answer)
```

## Sample Outputs

- **Data Quality Score:** Percentage of non-missing cells across the dataset
- **Top 10 Products by Sales:** Ranked product-level revenue breakdown
- **Sales by Region:** Interactive bar chart
- **Category Distribution:** Interactive pie chart
- **AI Business Report:** Gemini-generated insights covering risks, trends, and recommendations

## Key Features

- Modular multi-agent design — each agent is independently testable
- Natural language Q&A on tabular data via Gemini
- SQL interface on dataframes without a database setup
- Interactive Plotly charts rendered inline in Colab
- Automated data quality scoring

## Dataset

The project uses the **Sample Superstore** dataset, a commonly used retail analytics dataset containing order-level records with fields like Sales, Profit, Category, Region, and Product Name.

You can download it from [Kaggle](https://www.kaggle.com/).

## 🐙 Author

**Deeksha**
B.Tech ECE, Thapar Institute of Engineering and Technology
[GitHub](https://github.com/Deeksha2508)


