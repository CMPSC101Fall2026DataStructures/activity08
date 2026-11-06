# Tutorial 2: Data Visualization with CSV Files

## Overview

In this tutorial, you will learn how to load data from CSV files and create interactive visualizations using Streamlit. You will build a data dashboard that allows users to explore datasets through charts, plots, and heatmaps. This tutorial introduces data analysis concepts: loading data with Pandas, filtering datasets, and creating multiple types of visualizations.

This tutorial builds on Tutorial 1 by adding **data manipulation** and **visualization** capabilities to your Streamlit applications.

![--- --- --- --- --- --- --- --- ---](../graphics/div_bar.png)

## What You Will Learn

In this tutorial, you will learn to:

1. **Load CSV files** using Pandas within a Streamlit app
2. **Display data** in interactive tables that users can sort and filter
3. **Create visualizations** including line charts, bar charts, scatter plots, and heatmaps
4. **Let users interact with data** by selecting columns, filtering ranges, and choosing chart types
5. **Organize a multi-file data project** with separate data files for different analyses

### Real-World Context

Data dashboards are used everywhere: business intelligence teams use them to track sales, scientists use them to visualize experiments, and analysts use them to communicate insights. The skills you learn here are directly applicable to real-world data analysis projects.

Popular tools like Tableau, Power BI, and Google Data Studio do what you're about to do - but with Python and Streamlit, you have complete control and can customize everything.

![--- --- --- --- --- --- --- --- ---](../graphics/div_bar.png)

## Understanding the Data

This tutorial includes three CSV datasets:

1. **sales_data.csv** - Monthly sales data for different products
2. **weather_data.csv** - Daily temperature and weather measurements
3. **student_grades.csv** - Student performance data across different subjects

You can also bring your own CSV files to experiment with!

![--- --- --- --- --- --- --- --- ---](../graphics/div_bar.png)

## Part 1: Environment Setup

**Prerequisites**: Before starting this tutorial, you must complete the environment setup from **Tutorial 1**. If you haven't done so yet, go back to Tutorial 1 and follow the setup instructions in Part 1. That setup creates a shared virtual environment with all the packages needed for all three tutorials.

**Verification**: To verify your environment is set up correctly, make sure:

1. You've run `uv init` in the `09_activity_working` project root directory
2. You've installed all packages with: `uv add streamlit pandas matplotlib seaborn plotly wordcloud textblob nltk`

If you completed Tutorial 1, you're ready to proceed!

![--- --- --- --- --- --- --- --- ---](../graphics/div_bar.png)

## Part 2: Complete the Source File

Open `data_dashboard.py` in your code editor. You will see a template with `TODO` comments. Follow each step below to fill in the code.

### Step 1: Import Required Libraries

**What it does**: Imports Streamlit for the web app, Pandas for data manipulation, and visualization libraries.

Replace `# TODO: Add imports here` with:

```python
import streamlit as st
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns
import plotly.express as px
import plotly.graph_objects as go
```

**Explanation**:

- `streamlit` creates the web interface
- `pandas` (as `pd`) handles data loading and manipulation
- `matplotlib` and `seaborn` create static plots
- `plotly` creates interactive plots that users can hover over and zoom

![--- --- --- --- --- --- --- --- ---](../graphics/div_bar.png)

### Step 2: Configure the Page

**What it does**: Sets up the page with a wide layout for better data display.

Replace `# TODO: Configure the page` with:

```python
st.set_page_config(
    page_title="Data Visualization Dashboard",
    page_icon="📊",
    layout="wide"
)
```

**Explanation**: The `layout="wide"` parameter makes the app use the full browser width, which is better for displaying charts and tables side by side.

![--- --- --- --- --- --- --- --- ---](../graphics/div_bar.png)

### Step 3: Add Title and Introduction

**What it does**: Displays the dashboard title and instructions.

Replace `# TODO: Add title and introduction` with:

```python
st.title("📊 Data Visualization Dashboard")
st.write("""
This dashboard demonstrates how to load and visualize data from CSV files.
Select a dataset from the sidebar to begin exploring!
""")
```

![--- --- --- --- --- --- --- --- ---](../graphics/div_bar.png)

### Step 4: Create Dataset Selection in Sidebar

**What it does**: Adds a sidebar widget for selecting which dataset to analyze.

Replace `# TODO: Create sidebar for dataset selection` with:

```python
st.sidebar.header("📁 Dataset Selection")

dataset_option = st.sidebar.selectbox(
    "Choose a dataset:",
    ["Sales Data", "Weather Data", "Student Grades"]
)

st.sidebar.write("---")
st.sidebar.header("📈 Visualization Options")
```

**Explanation**: `st.sidebar` adds widgets to a collapsible sidebar, keeping the main area uncluttered. Users can select which dataset to explore.

![--- --- --- --- --- --- --- --- ---](../graphics/div_bar.png)

### Step 5: Load the Selected Dataset

**What it does**: Loads the CSV file based on the user's selection.

Replace `# TODO: Load data based on selection` with:

```python
@st.cache_data
def load_data(dataset_name):
    """Load data from CSV file and cache it for performance."""
    if dataset_name == "Sales Data":
        df = pd.read_csv("data/sales_data.csv")
    elif dataset_name == "Weather Data":
        df = pd.read_csv("data/weather_data.csv")
    else:  # Student Grades
        df = pd.read_csv("data/student_grades.csv")
    return df

# Load the selected dataset
df = load_data(dataset_option)
```

**Explanation**: The `@st.cache_data` decorator caches the loaded data so it doesn't reload every time the user interacts with a widget. This makes the app much faster. `pd.read_csv()` reads the CSV file and returns a DataFrame (Pandas' table structure).

![--- --- --- --- --- --- --- --- ---](../graphics/div_bar.png)

### Step 6: Display Dataset Overview

**What it does**: Shows basic information about the loaded dataset.

Replace `# TODO: Display dataset overview` with:

```python
st.header(f"📋 Dataset: {dataset_option}")

col1, col2, col3 = st.columns(3)

with col1:
    st.metric("Total Rows", len(df))
with col2:
    st.metric("Total Columns", len(df.columns))
with col3:
    st.metric("Memory Usage", f"{df.memory_usage(deep=True).sum() / 1024:.1f} KB")

# Show the first few rows
st.subheader("Data Preview")
st.dataframe(df.head(10), use_container_width=True)

# Show basic statistics
if st.checkbox("Show Statistical Summary"):
    st.subheader("Statistical Summary")
    st.dataframe(df.describe(), use_container_width=True)
```

**Explanation**:

- `st.columns(3)` creates three side-by-side columns for metrics
- `st.metric()` displays key statistics
- `df.head(10)` shows the first 10 rows
- `df.describe()` generates statistical summaries (mean, std, min, max, etc.)
- `st.dataframe()` displays interactive tables users can scroll and sort

![--- --- --- --- --- --- --- --- ---](../graphics/div_bar.png)

### Step 7: Create Visualizations Based on Dataset

**What it does**: Creates appropriate charts based on which dataset is selected.

Replace `# TODO: Create visualizations based on dataset` with:

```python
st.header("📊 Data Visualizations")

if dataset_option == "Sales Data":
    # Sales Data Visualizations
    
    st.subheader("1. Sales by Product (Bar Chart)")
    fig = px.bar(df, x="Product", y="Sales", color="Product",
                 title="Total Sales by Product")
    st.plotly_chart(fig, use_container_width=True)
    
    st.subheader("2. Sales Trends Over Time (Line Chart)")
    fig = px.line(df, x="Month", y="Sales", color="Product",
                  title="Monthly Sales Trends",
                  markers=True)
    st.plotly_chart(fig, use_container_width=True)
    
    st.subheader("3. Sales vs Advertising Spend (Scatter Plot)")
    fig = px.scatter(df, x="Advertising_Spend", y="Sales", color="Product",
                     size="Sales", hover_data=["Month"],
                     title="Sales vs Advertising Spend")
    st.plotly_chart(fig, use_container_width=True)
    
    # Interactive filtering
    st.subheader("4. Interactive Filter")
    min_sales = st.slider("Minimum Sales:", 
                          int(df["Sales"].min()), 
                          int(df["Sales"].max()), 
                          int(df["Sales"].min()))
    filtered_df = df[df["Sales"] >= min_sales]
    st.write(f"Showing {len(filtered_df)} records with sales >= ${min_sales}")
    st.dataframe(filtered_df, use_container_width=True)

elif dataset_option == "Weather Data":
    # Weather Data Visualizations
    
    st.subheader("1. Temperature Over Time (Line Chart)")
    fig = px.line(df, x="Date", y=["High_Temp", "Low_Temp"],
                  title="Daily Temperature Range",
                  labels={"value": "Temperature (°F)", "variable": "Measurement"})
    st.plotly_chart(fig, use_container_width=True)
    
    st.subheader("2. Temperature Distribution (Histogram)")
    fig = px.histogram(df, x="High_Temp", nbins=20,
                       title="Distribution of High Temperatures",
                       labels={"High_Temp": "Temperature (°F)"})
    st.plotly_chart(fig, use_container_width=True)
    
    st.subheader("3. Weather Conditions (Pie Chart)")
    condition_counts = df["Condition"].value_counts()
    fig = px.pie(values=condition_counts.values, 
                 names=condition_counts.index,
                 title="Distribution of Weather Conditions")
    st.plotly_chart(fig, use_container_width=True)
    
    st.subheader("4. Temperature Heatmap by Day")
    # Create a pivot table for heatmap
    df['Day_of_Week'] = pd.to_datetime(df['Date']).dt.day_name()
    df['Week'] = pd.to_datetime(df['Date']).dt.isocalendar().week
    pivot = df.pivot_table(values='High_Temp', index='Day_of_Week', 
                           columns='Week', aggfunc='mean')
    
    fig, ax = plt.subplots(figsize=(12, 6))
    sns.heatmap(pivot, annot=True, fmt=".1f", cmap="YlOrRd", ax=ax)
    ax.set_title("Average High Temperature by Day and Week")
    st.pyplot(fig)

else:  # Student Grades
    # Student Grades Visualizations
    
    st.subheader("1. Average Grades by Subject (Bar Chart)")
    avg_grades = df[["Math", "Science", "English", "History"]].mean()
    fig = px.bar(x=avg_grades.index, y=avg_grades.values,
                 labels={"x": "Subject", "y": "Average Grade"},
                 title="Average Grades by Subject")
    st.plotly_chart(fig, use_container_width=True)
    
    st.subheader("2. Grade Distribution (Box Plot)")
    # Melt the dataframe to long format for box plot
    df_melted = df.melt(id_vars=["Student"], 
                        value_vars=["Math", "Science", "English", "History"],
                        var_name="Subject", value_name="Grade")
    fig = px.box(df_melted, x="Subject", y="Grade",
                 title="Grade Distribution by Subject")
    st.plotly_chart(fig, use_container_width=True)
    
    st.subheader("3. Student Performance Heatmap")
    # Select only numeric columns for heatmap
    grade_cols = ["Math", "Science", "English", "History"]
    fig, ax = plt.subplots(figsize=(10, 8))
    sns.heatmap(df[grade_cols].T, annot=True, fmt=".0f", 
                cmap="RdYlGn", ax=ax, yticklabels=grade_cols)
    ax.set_title("Student Grades Heatmap")
    ax.set_xlabel("Student Index")
    st.pyplot(fig)
    
    st.subheader("4. Subject Correlation Matrix")
    fig, ax = plt.subplots(figsize=(8, 6))
    correlation = df[grade_cols].corr()
    sns.heatmap(correlation, annot=True, fmt=".2f", 
                cmap="coolwarm", center=0, ax=ax)
    ax.set_title("Correlation Between Subjects")
    st.pyplot(fig)
    
    # Student performance finder
    st.subheader("5. Find Student Performance")
    student_id = st.number_input("Enter Student ID:", 
                                 min_value=0, 
                                 max_value=len(df)-1, 
                                 value=0)
    if student_id < len(df):
        student_data = df.iloc[student_id]
        st.write(f"**Student:** {student_data['Student']}")
        
        grades = {
            "Math": student_data["Math"],
            "Science": student_data["Science"],
            "English": student_data["English"],
            "History": student_data["History"]
        }
        
        fig = px.bar(x=list(grades.keys()), y=list(grades.values()),
                     labels={"x": "Subject", "y": "Grade"},
                     title=f"Grades for {student_data['Student']}")
        st.plotly_chart(fig, use_container_width=True)
```

**Explanation**: This large section creates different visualizations depending on the selected dataset:

- **Sales Data**: Bar charts, line charts, and scatter plots
- **Weather Data**: Temperature trends, histograms, pie charts, and heatmaps
- **Student Grades**: Bar charts, box plots, heatmaps, and correlation matrices

Each visualization uses either Plotly (interactive) or Matplotlib/Seaborn (static but powerful for heatmaps).

![--- --- --- --- --- --- --- --- ---](../graphics/div_bar.png)

### Step 8: Add Chart Type Selector (Advanced Feature)

**What it does**: Lets users choose which type of chart to create for their data.

Replace `# TODO: Add custom chart creator` with:

```python
st.header("🎨 Custom Chart Creator")

st.write("Create your own visualization by selecting columns and chart type:")

chart_type = st.selectbox("Select chart type:", 
                          ["Line Chart", "Bar Chart", "Scatter Plot", "Area Chart"])

# Get numeric and categorical columns
numeric_cols = df.select_dtypes(include=['float64', 'int64']).columns.tolist()
all_cols = df.columns.tolist()

col1, col2 = st.columns(2)

with col1:
    x_axis = st.selectbox("X-axis:", all_cols)
with col2:
    y_axis = st.selectbox("Y-axis:", numeric_cols if numeric_cols else all_cols)

if st.button("Create Chart"):
    try:
        if chart_type == "Line Chart":
            fig = px.line(df, x=x_axis, y=y_axis, title=f"{y_axis} vs {x_axis}")
        elif chart_type == "Bar Chart":
            fig = px.bar(df, x=x_axis, y=y_axis, title=f"{y_axis} by {x_axis}")
        elif chart_type == "Scatter Plot":
            fig = px.scatter(df, x=x_axis, y=y_axis, title=f"{y_axis} vs {x_axis}")
        else:  # Area Chart
            fig = px.area(df, x=x_axis, y=y_axis, title=f"{y_axis} vs {x_axis}")
        
        st.plotly_chart(fig, use_container_width=True)
    except Exception as e:
        st.error(f"Could not create chart: {e}")
        st.write("Try selecting different columns or a different chart type.")
```

**Explanation**: This section gives users complete control to create their own charts by selecting:

- Chart type (line, bar, scatter, area)
- X-axis column
- Y-axis column

The `try-except` block handles errors gracefully if incompatible columns are selected.

![--- --- --- --- --- --- --- --- ---](../graphics/div_bar.png)

### Step 9: Add Data Export Feature

**What it does**: Allows users to download filtered or processed data.

Replace `# TODO: Add data export option` with:

```python
st.header("💾 Export Data")

st.write("Download the current dataset as a CSV file:")

csv = df.to_csv(index=False).encode('utf-8')

st.download_button(
    label="Download CSV",
    data=csv,
    file_name=f"{dataset_option.replace(' ', '_').lower()}_export.csv",
    mime="text/csv"
)
```

**Explanation**: `st.download_button()` creates a button that downloads data. We convert the DataFrame to CSV format using `to_csv()` and encode it as UTF-8. Users can download their filtered or analyzed data.

![--- --- --- --- --- --- --- --- ---](../graphics/div_bar.png)

### Step 10: Add Instructions and Tips

**What it does**: Provides helpful information for using the dashboard.

Replace `# TODO: Add tips and instructions` with:

```python
st.sidebar.write("---")
st.sidebar.header("💡 Tips")
st.sidebar.write("""
**Interaction Tips:**
- Hover over charts to see details
- Click and drag to zoom in
- Double-click charts to reset zoom
- Use filters to focus on specific data

**Bring Your Own Data:**
Place your CSV file in the `data/` folder and modify the code to load it!
""")

# Footer
st.write("---")
st.success("✅ Tutorial 2 Complete! You've learned data loading, visualization, and interactive filtering.")
```

**Explanation**: These tips help users understand how to interact with the dashboard and encourage experimentation with their own data.

![--- --- --- --- --- --- --- --- ---](../graphics/div_bar.png)

## Part 3: Run Your Data Dashboard

### For macOS and Linux:

Make sure you're in the project root directory (`09_activity_working`), then run:

```bash
uv run streamlit run src/tutorial_02_data_visualization/data_dashboard.py
```

### For Windows (Command Prompt or PowerShell):

Make sure you're in the project root directory (`09_activity_working`), then run:

```cmd
uv run streamlit run src\tutorial_02_data_visualization\data_dashboard.py
```

**What happens:**

1. Streamlit starts a local web server
2. Your browser opens to `http://localhost:8501`
3. You see your data dashboard with the default dataset loaded

**To stop the app:**

- Press `Ctrl+C` in the terminal

![--- --- --- --- --- --- --- --- ---](../graphics/div_bar.png)

## Part 4: Experiment and Explore

Try these activities:

1. **Switch datasets** - Use the sidebar to view different datasets
2. **Interact with charts** - Hover, zoom, and explore the visualizations
3. **Use filters** - Try the sales filter slider
4. **Create custom charts** - Use the custom chart creator
5. **Export data** - Download a CSV file
6. **Modify the code**:
   - Change chart colors
   - Add new visualization types
   - Create additional filters
   - Add your own CSV file and visualize it

![--- --- --- --- --- --- --- --- ---](../graphics/div_bar.png)

## Understanding Key Concepts

### DataFrames

A **DataFrame** is Pandas' primary data structure - think of it as a table with rows and columns, like an Excel spreadsheet. You can:

- Select columns: `df["Sales"]`
- Filter rows: `df[df["Sales"] > 1000]`
- Calculate statistics: `df["Sales"].mean()`
- Group and aggregate: `df.groupby("Product")["Sales"].sum()`

### Caching

The `@st.cache_data` decorator tells Streamlit to save ("cache") the result of a function. When the function is called again with the same parameters, Streamlit returns the cached result instead of rerunning the function. This is crucial for performance when loading large datasets.

### Interactive Charts

Plotly charts are interactive by default. Users can:

- Hover to see exact values
- Zoom in on specific ranges
- Pan to different areas
- Toggle series on and off
- Download chart images

This interactivity makes your dashboard much more useful than static images.

![--- --- --- --- --- --- --- --- ---](../graphics/div_bar.png)

## Key Takeaways

✅ **Pandas DataFrames** store and manipulate tabular data

✅ **st.cache_data** improves performance by caching loaded data

✅ **Plotly creates interactive charts** that users can explore

✅ **Matplotlib and Seaborn** are great for heatmaps and statistical visualizations

✅ **File upload and download** make dashboards practical for real work

✅ **Multiple visualization types** serve different purposes (trends, distributions, correlations, etc.)

![--- --- --- --- --- --- --- --- ---](../graphics/div_bar.png)

## Next Steps

You now know how to build data dashboards! In Tutorial 3, you will learn how to:

- Load and analyze text data
-Perform text analysis (word frequency, sentiment analysis)
- Create word clouds and text visualizations
- Extract insights from unstructured text

Continue to [Tutorial 3: Text Analysis with Streamlit](tutorial_03_text_analysis.md) when you're ready!
