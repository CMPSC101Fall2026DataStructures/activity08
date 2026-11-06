# Tutorial 1: Creating Your First Interactive Streamlit App

## Overview

In this tutorial, you will learn what Streamlit is and create your first interactive web application. You will write a simple program that demonstrates Streamlit's interactive widgets including buttons, sliders, balloons, and other toggles. This tutorial introduces the fundamental concepts of web-based data applications: reactive programming, widget state management, and real-time user interaction.

This tutorial assumes you have **never used Streamlit or built a web application before**. We will build your knowledge step by step.

![--- --- --- --- --- --- --- --- ---](../graphics/div_bar.png)

## What is Streamlit?

**Streamlit** is an open-source Python library that transforms Python scripts into interactive web applications. Here is what you need to know:

### The Problem It Solves

When data scientists and developers want to share their work, they face several challenges:

- Creating user interfaces requires learning HTML, CSS, and JavaScript
- Building interactive dashboards traditionally takes weeks or months
- Deploying web applications requires server configuration and hosting
- Iterating on designs is slow and cumbersome

### The Streamlit Solution

Streamlit handles these concerns with a simple, Pythonic API:

1. **Write Pure Python** - No HTML, CSS, or JavaScript required
2. **Instant Reactivity** - The app automatically reruns when users interact with widgets
3. **Built-in Widgets** - Buttons, sliders, text inputs, and more are ready to use
4. **Hot Reloading** - Changes to your code appear immediately in the browser

Together, these features let you turn a data script into a shareable application in minutes, not weeks.

### Real-World Context

Streamlit is used by data scientists at companies like Uber, Twitter, and Netflix to quickly prototype dashboards and share insights with stakeholders. The patterns you learn here - reactive programming, state management, and interactive widgets - are fundamental to modern web development.

![--- --- --- --- --- --- --- --- ---](../graphics/div_bar.png)

## What is Reactive Programming?

**Reactive programming** means that your application automatically responds to user input. In Streamlit:

1. User interacts with a widget (clicks a button, moves a slider)
2. Streamlit **reruns your entire Python script** from top to bottom
3. The updated output appears in the browser

This is different from traditional programming where you must explicitly tell the program to update when something changes. Streamlit handles the updates for you automatically.

![--- --- --- --- --- --- --- --- ---](../graphics/div_bar.png)

## Part 1: Set Up the Project Environment

**Note**: This setup will create a shared virtual environment for **all three tutorials**. You only need to do this once.

### For macOS and Linux:

Navigate to the project root directory. Replace `09_activity_repository/` with what your repository is called.

```bash
cd 09_activity_repository/
```

Initialize the project with UV (this creates a virtual environment):

```bash
uv init
```

Install all required packages for all three tutorials:

```bash
uv add streamlit pandas matplotlib seaborn plotly wordcloud textblob nltk
```

### For Windows (Command Prompt):

Navigate to the project root directory:

```cmd
cd 09_activity_repository
```

Initialize the project with UV:

```cmd
uv init
```

Install all required packages for all three tutorials:

```cmd
uv add streamlit pandas matplotlib seaborn plotly wordcloud textblob nltk
```

### For Windows (PowerShell):

Navigate to the project root directory:

```powershell
cd 09_activity_repository
```

Initialize the project with UV:

```powershell
uv init
```

Install all required packages for all three tutorials:

```powershell
uv add streamlit pandas matplotlib seaborn plotly wordcloud textblob nltk
```

![--- --- --- --- --- --- --- --- ---](../graphics/div_bar.png)

## Part 2: Complete the Source File

Open `interactive_app.py` in your code editor. You will see a template with `TODO` comments. Follow each step below to fill in the code.

### Step 1: Import Streamlit

**What it does**: Makes the Streamlit library available in this file.

Replace `# TODO: Add imports here` with:

```python
import streamlit as st
```

**Explanation**: The `streamlit` module provides everything needed to create web applications: widgets, layout tools, and display functions. We import it as `st` for convenience, following the Streamlit community convention.

![--- --- --- --- --- --- --- --- ---](../graphics/div_bar.png)

### Step 2: Set the Page Title and Header

**What it does**: Configures the browser tab title and displays a large heading on the page.

Replace `# TODO: Set page configuration` with:

```python
st.set_page_config(page_title="My First Streamlit App", page_icon="🎈")
```

**Explanation**: `st.set_page_config()` must be called before any other Streamlit command. It sets the browser tab title and favicon (the small icon in the tab).

Replace `# TODO: Add title and description` with:

```python
st.title("🎈 Welcome to My First Streamlit App!")
st.write("This tutorial demonstrates Streamlit's interactive widgets and features.")
```

**Explanation**: `st.title()` creates a large heading. `st.write()` is Streamlit's "magic" function - it automatically formats whatever you pass it. Text becomes paragraphs, dataframes become tables, and more.

![--- --- --- --- --- --- --- --- ---](../graphics/div_bar.png)

### Step 3: Add Interactive Widgets

**What it does**: Creates buttons, sliders, and other interactive elements.

Replace `# TODO: Add a button that triggers balloons` with:

```python
st.header("🎯 Interactive Elements")

if st.button("🎉 Celebrate!"):
    st.balloons()
    st.success("Celebration activated! 🎊")
```

**Explanation**: `st.button()` creates a clickable button. It returns `True` when clicked, `False` otherwise. The `if` statement checks if the button was clicked. `st.balloons()` displays a fun balloon animation. `st.success()` shows a green success message.

Replace `# TODO: Add a slider` with:

```python
st.header("🎚️ Slider Control")

value = st.slider("Select a number:", min_value=0, max_value=100, value=50)
st.write(f"You selected: **{value}**")

if value > 75:
    st.info("That's a high number! 📈")
elif value < 25:
    st.info("That's a low number! 📉")
else:
    st.info("That's a medium number! 📊")
```

**Explanation**: `st.slider()` creates a slider widget. It returns the current value. The `min_value`, `max_value`, and `value` parameters control the range and starting position. We use the value to display different messages.

Replace `# TODO: Add a text input` with:

```python
st.header("✏️ Text Input")

name = st.text_input("What's your name?", placeholder="Enter your name...")

if name:
    st.write(f"Hello, **{name}**! 👋")
    if st.button("Say Goodbye"):
        st.write(f"Goodbye, {name}! See you next time! 👋")
```

**Explanation**: `st.text_input()` creates a text input field. The `placeholder` parameter shows hint text. We check `if name:` to display a greeting only when the user has entered text.

Replace `# TODO: Add a selectbox (dropdown menu)` with:

```python
st.header("📋 Selection Menu")

color = st.selectbox(
    "Choose your favorite color:",
    ["Red", "Green", "Blue", "Yellow", "Purple"]
)

st.write(f"Your favorite color is: **{color}**")

# Display a colored message box based on selection
if color == "Red":
    st.error("Red is bold and energetic! ❤️")
elif color == "Green":
    st.success("Green is calm and natural! 💚")
elif color == "Blue":
    st.info("Blue is cool and peaceful! 💙")
elif color == "Yellow":
    st.warning("Yellow is bright and cheerful! 💛")
else:
    st.write("Purple is creative and mysterious! 💜")
```

**Explanation**: `st.selectbox()` creates a dropdown menu. Users can pick one option from the list. We use the selected value to show different colored message boxes.

Replace `# TODO: Add a checkbox` with:

```python
st.header("✅ Checkbox Options")

show_code = st.checkbox("Show Python code example")

if show_code:
    st.code("""
# This is a Python code example
def greet(name):
    return f"Hello, {name}!"

message = greet("Student")
print(message)
    """, language="python")
```

**Explanation**: `st.checkbox()` creates a checkbox that toggles between checked and unchecked. It returns `True` when checked, `False` when unchecked. `st.code()` displays formatted code with syntax highlighting.

Replace `# TODO: Add radio buttons` with:

```python
st.header("🔘 Radio Buttons")

mood = st.radio(
    "How are you feeling today?",
    ["Happy 😊", "Excited 🤩", "Calm 😌", "Tired 😴"]
)

st.write(f"You're feeling: **{mood}**")
```

**Explanation**: `st.radio()` creates radio buttons where only one option can be selected at a time. This is useful for multiple-choice questions.

Replace `# TODO: Add a multiselect` with:

```python
st.header("🎯 Multi-Select")

interests = st.multiselect(
    "Select your interests (you can choose multiple):",
    ["Programming", "Data Science", "Web Development", "Machine Learning", "Game Development", "Cybersecurity"]
)

if interests:
    st.write(f"You selected **{len(interests)}** interest(s):")
    for interest in interests:
        st.write(f"- {interest}")
else:
    st.write("No interests selected yet.")
```

**Explanation**: `st.multiselect()` allows users to select multiple options from a list. It returns a list of selected items. We check if the list is empty and display the selections.

Replace `# TODO: Add columns layout` with:

```python
st.header("📊 Layout with Columns")

col1, col2, col3 = st.columns(3)

with col1:
    st.metric(label="Temperature", value="72°F", delta="1.2°F")

with col2:
    st.metric(label="Wind Speed", value="9 mph", delta="-1 mph")

with col3:
    st.metric(label="Humidity", value="65%", delta="3%")
```

**Explanation**: `st.columns()` creates side-by-side columns for layout. `st.metric()` displays a metric with a value and change indicator. The `delta` parameter shows whether the value increased or decreased.

Replace `# TODO: Add an expander` with:

```python
st.header("📦 Expandable Section")

with st.expander("Click to learn more about Streamlit"):
    st.write("""
        Streamlit is an open-source Python library that makes it easy to create and share 
        beautiful, custom web apps for machine learning and data science. In just a few minutes, 
        you can build and deploy powerful data apps.
        
        **Key Features:**
        - Pure Python - no HTML/CSS/JavaScript required
        - Instant reactivity - automatic updates when inputs change
        - Built-in widgets - buttons, sliders, charts, and more
        - Easy deployment - share your apps with one command
    """)
```

**Explanation**: `st.expander()` creates a collapsible section that users can expand or collapse. This is useful for hiding detailed information that not all users need to see.

Replace `# TODO: Add a progress bar` with:

```python
st.header("⏳ Progress Bar")

if st.button("Run Progress Bar"):
    import time
    progress_bar = st.progress(0)
    status_text = st.empty()
    
    for i in range(101):
        progress_bar.progress(i)
        status_text.text(f"Loading... {i}%")
        time.sleep(0.02)
    
    status_text.text("Complete! ✅")
```

**Explanation**: `st.progress()` displays a progress bar. `st.empty()` creates a placeholder that can be updated. We use a loop to simulate a loading process and update the progress bar.

Replace `# TODO: Add a final message` with:

```python
st.header("🎓 Congratulations!")

st.success("You've completed Tutorial 1! You now understand:")
st.write("""
- How to import and use Streamlit
- How to create basic interactive widgets (buttons, sliders, text inputs)
- How to use layout tools (columns, expanders)
- How Streamlit's reactive programming model works

**Next Steps:** Move on to Tutorial 2 to learn how to load and visualize data from CSV files!
""")
```

**Explanation**: This displays a congratulatory message and summarizes what was learned.

![--- --- --- --- --- --- --- --- ---](../graphics/div_bar.png)

## Part 3: Run Your Streamlit App

### For macOS and Linux:

Make sure you're in the project root directory (`09_activity_repository`), then run:

```bash
uv run streamlit run src/tutorial_01_interactive_streamlit/interactive_app.py
```

### For Windows (Command Prompt or PowerShell):

Make sure you're in the project root directory (`09_activity_repository`), then run:

```cmd
uv run streamlit run src\tutorial_01_interactive_streamlit\interactive_app.py
```

**What happens:**

1. Streamlit starts a local web server
2. Your default browser opens automatically
3. You see your interactive app running at `http://localhost:8501`

**To stop the app:**

- Press `Ctrl+C` in the terminal (works on all operating systems)

![--- --- --- --- --- --- --- --- ---](../graphics/div_bar.png)

## Part 4: Experiment and Explore

Now that your app is running, try these experiments:

1. **Click the "Celebrate!" button** - Watch the balloons animation
2. **Move the slider** - See how messages change based on the value
3. **Enter your name** - Watch the greeting appear in real-time
4. **Change widget values** - Notice how the app instantly updates (reactive programming!)
5. **Check the "Show Python code example" checkbox** - See formatted code
6. **Try the multi-select** - Select multiple interests
7. **Click "Run Progress Bar"** - Watch the animated progress

### Challenge: Make Your Own Modifications

Try making these changes to the code:

1. Change the slider range to 0-200
2. Add your own color to the selectbox
3. Change the metric labels to show different data
4. Add a new button that displays a different message
5. Create your own expander with different content

![--- --- --- --- --- --- --- --- ---](../graphics/div_bar.png)

## Understanding Streamlit's Execution Model

**Important Concept:** Every time you interact with a widget, Streamlit reruns your entire script from top to bottom. This is why your app is always in sync with the latest user input.

For example:

1. User moves slider to 80
2. Streamlit reruns the entire `interactive_app.py` file
3. When the script reaches `st.slider()`, it reads the value from the browser (80)
4. Your code executes with `value = 80`
5. The updated output appears in the browser

This "rerun on interaction" model is what makes Streamlit so simple and powerful. You don't need to write update handlers or manage state manually - Streamlit does it for you.

![--- --- --- --- --- --- --- --- ---](../graphics/div_bar.png)

## Key Takeaways

✅ **Streamlit transforms Python scripts into web apps** without requiring HTML/CSS/JavaScript

✅ **Reactive programming** means the app automatically reruns when users interact with widgets

✅ **Widgets return values** that you can use in your code (buttons return True/False, sliders return numbers, etc.)

✅ **Layout tools** like columns and expanders help organize your app

✅ **The app runs in a browser** but you write pure Python code

![--- --- --- --- --- --- --- --- ---](../graphics/div_bar.png)

## Next Steps

You now understand the basics of Streamlit! In Tutorial 2, you will learn how to:

- Load data from CSV files using Pandas
- Create interactive visualizations (line charts, bar charts, heatmaps)
- Let users filter and explore real datasets
- Build a complete data dashboard

Continue to [Tutorial 2: Data Visualization with CSV Files](tutorial_02_data_visualization.md) when you're ready!
