Keyboard Interaction Time-Series Analysis
Time-Domain & Frequency-Domain Analysis of Keystroke Timing Data

<p align="center">
<img src="https://img.shields.io/badge/Python-3.12-blue?logo=python&logoColor=white" alt="Python 3.12">
<img src="https://img.shields.io/badge/NumPy-FFT-013243?logo=numpy" alt="NumPy FFT">
<img src="https://img.shields.io/badge/Pandas-Data%20Analysis-150458?logo=pandas" alt="Pandas">
<img src="https://img.shields.io/badge/Matplotlib-Visualization-11557C" alt="Matplotlib">
<img src="https://img.shields.io/badge/Project-HCI%20Lab-orange" alt="HCI Lab Project">
</p>

About the Project

This project explores keyboard interaction patterns using time-series analysis of keystroke timing measurements from the Carnegie Mellon University (CMU) Keystroke Dynamics Benchmark.

It combines statistical analysis and signal processing to investigate how key hold durations vary across repeated typing trials.

The project implements two complementary approaches:

Approach	Purpose
Time-Domain Analysis	Summarizes hold durations using descriptive statistics and visualizes variation across repetitions.
Frequency-Domain Analysis	Applies the Fast Fourier Transform (FFT) to explore variation across repetition-order frequencies.
Objective: Understand how statistical methods and signal processing techniques can be applied to keyboard interaction measurements using Python.
Research Question

How can time-domain statistics and frequency-domain analysis characterize variation in a keyboard timing feature across repeated typing trials?

📂 Dataset

Source: CMU Keystroke Dynamics Benchmark

The dataset contains:

20,400 keystroke records
51 participants
8 sessions per participant
400 password repetitions per participant
50 repetitions per session
Features Used
Feature	Description
subject	Participant identifier
sessionIndex	Session number
rep	Repetition number within a session
H.period	Hold duration of the period (.) key

The analysis focuses on participant s002, session 1, using 50 observations of the H.period feature.

Dataset Setup

The dataset is not included in this repository. Download it from the official CMU source and place the CSV file in the following location:

text
data/DSL-StrongPasswordData.csv


Please consult the original dataset documentation for attribution and reuse terms.

⚙️ Methodology
1. Data Preparation
Load the CSV dataset using Pandas.
Inspect its structure and check for missing values.
Select participant s002 and session 1.
Extract the H.period feature.
Sort the observations by repetition number.
2. Time-Domain Analysis

Calculate the following descriptive statistics:

Mean
Standard deviation
Minimum
Maximum
Median

A line plot illustrates hold duration across repetitions, with a horizontal line marking the mean.

Output: outputs/time_domain_H_period.png

3. Frequency-Domain Analysis (FFT)

The FFT analysis follows these steps:

Remove the linear trend using SciPy.
Apply a Hann window to reduce spectral leakage.
Compute the one-sided FFT using rfft.
Calculate frequency bins using rfftfreq.
Estimate the amplitude spectrum.
Identify the strongest nonzero frequency component.
Calculate the corresponding approximate period.
Plot the spectrum and highlight the dominant frequency.

Output: outputs/fft_H_period.png

Results
Time-Domain Analysis

The following statistics were obtained for the 50 selected observations.

Metric	Value
Number of observations	50
Mean	0.111288 s
Standard deviation	0.015222 s
Minimum	0.077600 s
Maximum	0.149100 s
Median	0.111800 s

Key observation: The average hold duration was approximately 111.3 milliseconds, with a standard deviation of approximately 15.2 milliseconds.

Frequency-Domain Analysis
Metric	Value
Frequency resolution	0.0200 cycles/repetition
Dominant nonzero frequency	0.3600 cycles/repetition
Approximate spectral period	2.78 repetitions
Peak amplitude	0.008922 s (approximate)

Key observation: The strongest nonzero spectral component occurred at 0.36 cycles per repetition, corresponding to approximately 2.78 repetitions per cycle.

This is an exploratory finding and does not establish a stable periodic typing behavior.

Visualizations
Time-Domain Plot

File: outputs/time_domain_H_period.png

Displays key hold duration against repetition number. The dashed horizontal line represents the mean hold duration.

!Time-domain analysis of H.period

Frequency-Domain Plot

File: outputs/fft_H_period.png

Displays the one-sided FFT amplitude spectrum after detrending and Hann windowing. The dominant nonzero frequency is highlighted.

!FFT amplitude spectrum of H.period

🗂️ Project Structure
text
Keyboard_interaction/
│
├── data/
│   └── DSL-StrongPasswordData.csv
│
├── notebooks/
│   └── time_series_analysis.ipynb
│
├── outputs/
│   ├── time_domain_H_period.png
│   └── fft_H_period.png
│
├── src/
│   └── inspect_data.py
│
├── .gitignore
├── README.md
└── requirements.txt

Directory / File	Description
data/	Locally stored dataset
notebooks/	Jupyter Notebook containing the analysis
outputs/	Generated visualization files
src/	Supporting Python scripts
requirements.txt	Python dependencies
README.md	Project documentation
Note: Do not commit the dataset to version control unless its redistribution terms have been verified.
Getting Started
Prerequisites
Python 3.12 or a compatible version
pip
Jupyter Notebook
Step 1 — Navigate to the Project

Open Command Prompt on Windows:

cmd
cd /d "C:\HCI LAB\Keyboard_interaction"


Replace the path with your actual project directory if necessary.

Step 2 — Install Dependencies
bash
python -m pip install -r requirements.txt


If requirements.txt does not exist, create it with the following contents:

text
pandas
numpy
matplotlib
scipy
jupyter
ipykernel

Step 3 — Launch Jupyter Notebook
bash
python -m jupyter notebook

Step 4 — Run the Analysis

Open:

text
notebooks/time_series_analysis.ipynb


Run all cells from top to bottom.

The notebook will load the dataset, calculate statistics, perform FFT analysis, generate both plots, and verify that the output files have been saved.

Important: Ensure that data/DSL-StrongPasswordData.csv exists before running the notebook.

Limitations
The detailed analysis covers only one participant, one session, and 50 repetitions.
Results cannot be generalized to all participants or keyboard interactions.
Repetition order is not equivalent to continuous-time sampling.
FFT frequencies are expressed in cycles per repetition, not hertz.
A dominant spectral peak does not prove the existence of a stable behavioral cycle.
Results may depend on the selected feature and preprocessing methods.
The project does not implement or evaluate a keystroke-based authentication system.

The results should be interpreted as an educational demonstration of time-domain and frequency-domain analysis.


Attribution

Dataset: CMU Keystroke Dynamics Benchmark.

The dataset was developed for research into keystroke dynamics. This project uses the dataset for an educational analysis involving descriptive statistics, time-series visualization, and FFT.

It is not a reproduction of the benchmark's original anomaly-detection evaluation.

Consult the original CMU dataset documentation for the appropriate citation and reuse terms.

License

The license for this project's analysis code has not yet been specified. Dataset reuse and redistribution remain subject to the original dataset's terms. The code and dataset should not be assumed to share the same license.

<p align="center">
<i>Developed as part of a Human-Computer Interaction (HCI) lab project.</i>
<br>
<b>Python · Pandas · NumPy · SciPy · Matplotlib · Jupyter Notebook</b>
</p>
