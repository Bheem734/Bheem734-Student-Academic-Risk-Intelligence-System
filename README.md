Student Academic Risk Intelligence System

A data-driven application designed to analyze student academic performance and identify students who may require additional academic support. The system uses the UCI Student Performance (Maths) dataset and combines data preprocessing, feature engineering, visualization, analytics, REST APIs, and an interactive dashboard.

Overview

The system helps identify students who may be academically vulnerable by analyzing their academic records, study habits, attendance, family background, and lifestyle-related information.

The project is designed to:

Categorize students into Pass, Fail, or Dropout based on their final grade.
Calculate an academic risk score using failures, absences, alcohol consumption, and study time.
Identify students who are performing below the expected level.
Highlight students with strong academic performance.
Estimate a student's expected final grade using available academic and behavioral information.
Main Features
Data Preparation and Feature Engineering — Creates additional analytical features such as Result, Percentage, avg_alcohol, parent_edu_avg, grade_trend, total_support, risk_score, and g1_g2_avg.
Data Visualization — Produces static charts using Matplotlib and interactive visualizations using Plotly.
REST API — Provides a FastAPI-based service for retrieving student statistics, identifying at-risk students, finding top-performing students, and estimating student results.
Interactive Dashboard — Provides a Streamlit interface containing summary metrics, charts, filters, student information, and an at-risk student section.
Batch Analysis — Runs the complete analysis process from the command line and generates the required reports and charts.
Project Structure
Student-Academic-Risk-Intelligence-System/

├── analysis.py
├── app.py
├── main.py
├── requirements.txt
├── data/
│   └── Maths.csv
└── output/
File Description
analysis.py — Performs data loading, feature engineering, statistical analysis, and chart generation.
app.py — Runs the Streamlit-based interactive dashboard.
main.py — Contains the FastAPI REST API.
requirements.txt — Contains the Python packages required by the project.
data/Maths.csv — Contains the UCI Student Performance Maths dataset.
output/ — Stores charts generated during analysis.
Dataset

The project uses the UCI Student Performance Dataset for Mathematics. The dataset contains information related to student demographics, family circumstances, study behavior, lifestyle factors, academic support, and grades.

Important academic columns include:

G1 — First-period grade
G2 — Second-period grade
G3 — Final grade

The grades are measured on a scale from 0 to 20.

Student Result Classification

The final grade G3 is converted into three outcome categories:

G3 Range	Classification
0	Dropout
1–9	Fail
10–20	Pass

A final grade of 0 is therefore treated as a Dropout category, rather than simply being considered a zero academic score.

Installation

Install the project dependencies using:

pip install -r requirements.txt

The project requires:

Python 3.8+
pandas
numpy
matplotlib
plotly
streamlit
fastapi
uvicorn
pydantic
Running the Project
1. Run Data Analysis

Run:

python analysis.py

This performs the data analysis, calculates the main statistics, creates the Matplotlib charts, saves them inside the output directory, and displays the interactive Plotly visualizations.

2. Start the REST API

Run:

python main.py

Alternatively:

uvicorn main:app --reload

The API can then be accessed through:

http://localhost:8000

The interactive API documentation is available at:

http://localhost:8000/docs
API Endpoints
Method	Endpoint	Purpose
GET	/	Displays basic API information
GET	/summary	Returns overall student statistics
GET	/at-risk	Lists students whose final grade is between 1 and 9
GET	/top-students	Returns the highest-performing students
POST	/predict-result	Estimates the final grade using student information
Prediction Request Example
{
    "G1": 12,
    "G2": 13,
    "studytime": 2,
    "absences": 4,
    "failures": 0
}

The prediction endpoint uses these inputs to provide an estimated academic result.

3. Start the Dashboard

Run:

streamlit run app.py

The dashboard provides an interactive interface where users can view:

Total number of students
Average final grade
Pass percentage
Number of at-risk students
Number of dropouts
Study-time performance charts
Internet-access performance comparison
Filterable student records
At-risk student information
Engineered Features
Feature	Meaning
Result	Categorizes students as Pass, Fail, or Dropout according to G3
Percentage	Converts the final grade into a percentage of the 20-point scale
avg_alcohol	Average of weekday and weekend alcohol consumption
parent_edu_avg	Average education level of the student's mother and father
grade_trend	Difference between the final grade and the first-period grade
total_support	Number of positive responses for school support, family support, and paid classes
risk_score	Combined risk indicator based on failures, absences, alcohol consumption, and study time
g1_g2_avg	Average score of the first and second academic periods
Risk Score

The project calculates the risk indicator using:

(failures × 2) + (absences / 10) + avg_alcohol − studytime

A higher calculated value represents a greater level of academic risk according to the project's defined scoring approach.

Purpose of the System

The primary goal of the project is to transform raw student records into useful academic insights. By combining statistical analysis, visualization, APIs, and a dashboard, the system provides a practical way to explore student performance and identify students who may benefit from additional academic attention.

License

The project uses the publicly available UCI Student Performance Dataset for educational and analytical purposes.