# Source Code for Activity 09

This directory contains the source code for all three Streamlit tutorials.

## Directory Structure

```
src/
├── tutorial_01_interactive_streamlit/
│   ├── interactive_app.py          # Interactive widgets application
│   └── README.md                   # Tutorial 1 instructions
│
├── tutorial_02_data_visualization/
│   ├── data_dashboard.py           # Data visualization dashboard
│   ├── data/                       # Sample CSV datasets
│   │   ├── sales_data.csv
│   │   ├── weather_data.csv
│   │   └── student_grades.csv
│   └── README.md                   # Tutorial 2 instructions
│
└── tutorial_03_text_analysis/
    ├── text_analyzer.py            # Text analysis tool
    ├── data/                       # Sample text files
    │   ├── sample_review.txt
    │   ├── sample_article.txt
    │   └── sample_story.txt
    └── README.md                   # Tutorial 3 instructions
```

## Getting Started

1. Read the main [README.md](../README.md) for setup instructions
2. Set up the virtual environment at the project root (see main README)
3. Complete tutorials in order (1, 2, then 3)
4. Each tutorial directory has its own README with specific instructions

## Running the Applications

From each tutorial directory, use:

```bash
uv run streamlit run <application_name>.py
```

For example:
```bash
cd tutorial_01_interactive_streamlit/
uv run streamlit run interactive_app.py
```

## Tips

- Read the tutorial documents in the `tutorials/` folder for detailed explanations
- Complete TODO items in order
- Save your file and Streamlit will automatically reload
- Press `Ctrl+C` to stop the server
- Check terminal output for error messages

## Need Help?

Refer to the detailed tutorial documents in the `tutorials/` folder for step-by-step instructions and explanations of every code section.
