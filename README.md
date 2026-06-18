#  AI-Powered Data Analytics Agent

An agentic AI pipeline built in Python that automates the end-to-end data analytics workflow — from data ingestion and cleaning to SQL querying, visualization, and AI-generated business insights — powered by **Google Gemini 2.5 Flash**.

---

##  Overview

This project implements a multi-agent architecture where each agent handles a distinct stage of the analytics pipeline. Instead of writing monolithic analysis scripts, each responsibility is encapsulated in a dedicated agent class, making the system modular, extensible, and easy to debug.

The pipeline was built and tested on the classic **Superstore Sales Dataset** but can be adapted to any structured CSV data.

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
| `InsightAgent` | Calls Gemini API to generate business insights from the data summary |
| `QueryAgent` | Answers natural language questions about the dataset using Gemini |

---

##  Tech Stack

- **Language:** Python 3
- **Environment:** Google Colab
- **AI Model:** Google Gemini 2.5 Flash (`google-generativeai`)
- **Data Processing:** Pandas, NumPy
- **SQL on DataFrames:** pandasql
- **Visualization:** Plotly Express
- **File Handling:** openpyxl
  ---

## Setup & Installation

### 1. Clone the repository

```bash
git clone https://github.com/your-username/ai-data-analytics-agent.git
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

> Get a free API key at [Google AI Studio](https://aistudio.google.com/app/apikey).

### 4. Upload your dataset

Place `Superstore.csv` in your working directory, or upload it via Colab's file upload cell.

---

##  Pipeline Walkthrough

### Phase 1 — Data Ingestion & Cleaning

```python
df = ingestion_agent.load_data("Superstore.csv")
df = cleaning_agent.clean(df)
```

### Phase 2 — Data Quality Report

```python
quality_report = quality_agent.generate_report(df)
# Outputs: missing values, duplicate rows, data types, quality score (%)
```

### Phase 3 — Analytics

```python
analytics_agent.total_sales(df)
analytics_agent.total_profit(df)
analytics_agent.top_products(df)
```

### Phase 4 — SQL Queries

```python
query = """
SELECT Category, SUM(Sales) as TotalSales
FROM df
GROUP BY Category
ORDER BY TotalSales DESC
"""
sql_agent.execute_query(query, df)
```

### Phase 5 — Visualization

```python
visualization_agent.sales_by_region(df)   # Bar chart
visualization_agent.category_sales(df)    # Pie chart
```

### Phase 6 — AI Insights (Gemini)

```python
insights = insight_agent.generate_insights(df)
print(insights)
# Returns: key insights, business risks, growth opportunities, recommendations
```

### Phase 7 — Natural Language Querying

```python
answer = query_agent.answer_question(df, "Which region has the highest profit margin?")
print(answer)
```

---

## Sample Outputs

- **Data Quality Score:** Percentage of non-missing cells across the dataset
- **Top 10 Products by Sales:** Ranked product-level revenue breakdown
- **Sales by Region:** Interactive bar chart
- **Category Distribution:** Interactive pie chart
- **AI Business Report:** Gemini-generated insights covering risks, trends, and recommendations

---

##  Key Features

- Modular multi-agent design — each agent is independently testable
- Natural language Q&A on tabular data via Gemini
- SQL interface on dataframes without a database setup
- Interactive Plotly charts rendered inline in Colab
- Automated data quality scoring

---

## Dataset

The project uses the **Sample Superstore** dataset, a commonly used retail analytics dataset containing order-level records with fields like Sales, Profit, Category, Region, and Product Name.

You can download it from [Kaggle](https://www.kaggle.com/datasets/vivek468/superstore-dataset-final).

---

## 🙋‍♀️ Author

**Deeksha**  
B.Tech ECE, Thapar Institute of Engineering and Technology  
[GitHub](https://github.com/Deeksha2508/) 

---



## 📂 Project Structure
