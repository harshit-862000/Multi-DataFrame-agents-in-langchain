# 🤖 Multi DataFrame Agent using LangChain

This project demonstrates how to build an **AI-powered agent** using LangChain that can interact with **single and multiple Pandas DataFrames** using natural language queries.

It leverages:

* 🧠 LLM (via OpenRouter)
* 🐼 Pandas DataFrames
* ⚡ LangChain Agents

---

## 🚀 Overview

The agent can:

* Analyze datasets using plain English queries
* Perform calculations and comparisons
* Work with **multiple DataFrames simultaneously**
* Automatically generate Python code to answer queries

---

## 🛠️ Tech Stack

* Python
* LangChain (`langchain`, `langchain_experimental`)
* Pandas
* OpenRouter (LLM provider)

---

## 📦 Installation

```bash
pip install langchain langchain_experimental pandas openai
```

---

## 🔑 Setup (OpenRouter)

```python
import os

os.environ["OPENAI_API_KEY"] = "your-openrouter-api-key"
os.environ["OPENAI_API_BASE"] = "https://openrouter.ai/api/v1"
```

---

## 📊 Dataset

The project uses the Titanic dataset:

```python
url = "https://raw.githubusercontent.com/adamerose/datasets/master/titanic.csv"
df = pd.read_csv(url)
```

---

## 🤖 Single DataFrame Agent

```python
from langchain_experimental.agents.agent_toolkits import create_pandas_dataframe_agent
from langchain_community.llms import OpenAI

llm = OpenAI()

agent = create_pandas_dataframe_agent(
    llm,
    df,
    verbose=True,
    allow_dangerous_code=True
)

agent.run("How many people have age greater than 23?")
```

---

## 🔗 Multi DataFrame Agent

```python
df1 = df.copy()

# Fill missing values
df['age'] = df1['age'].fillna(df1["age"].mean())

agent = create_pandas_dataframe_agent(
    llm,
    [df, df1],
    verbose=True,
    allow_dangerous_code=True
)

agent.run("How many rows in the age column are different?")
```

---

## ➕ Additional Data Processing

```python
df2 = df1.copy()
df2["Age_multiplied"] = df1["age"] * 2

agent.run("Are the number of columns same in all dataframes?")
```

---

## 🧠 How It Works

* The agent converts natural language → Python code
* Executes code on DataFrames
* Returns results in human-readable form

---

## ⚠️ Important Notes

* `allow_dangerous_code=True` enables code execution → use carefully
* Ensure API keys are kept secure (do NOT expose in public repos)
* Works best with structured/tabular data

---

## 🔥 Features

* Natural language querying of data
* Multi-dataframe comparison
* Automatic data analysis
* No need to write Pandas code manually

---

## 🚀 Future Improvements

* Add Streamlit UI for interactive queries
* Integrate multiple datasets dynamically
* Add visualization support (matplotlib / seaborn)
* Use ChatOpenAI instead of legacy OpenAI class

---

## 📌 Example Queries

* "How many people are older than 23?"
* "Compare age columns between datasets"
* "Are column counts same across DataFrames?"

---

## 📜 License

MIT License
