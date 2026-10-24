Keyboard Interaction Time-Series Analysis
Time-Domain and Frequency-Domain (FFT) Analysis of Keystroke Timing Data

A small Human-Computer Interaction (HCI) lab project exploring keyboard interaction measurements using descriptive statistics, time-series visualization, and the Fast Fourier Transform (FFT).

Project Overview

This project analyzes keystroke timing data from the Carnegie Mellon University (CMU) Keystroke Dynamics Benchmark. It demonstrates two complementary approaches to time-series analysis:

Time-domain analysis: Uses descriptive statistics to summarize key hold durations, including the mean, standard deviation, minimum, maximum, and median.
Frequency-domain analysis: Applies the Fast Fourier Transform (FFT) to an ordered sequence of measurements to investigate how variation is distributed across repetition-order frequencies.

The project provides a simple, reproducible example of numerical data analysis using Python. It is intended for educational purposes and does not implement a keyboard-based authentication system.

Research Question

How can time-domain statistics and frequency-domain analysis characterize variation in a keyboard timing feature across repeated typing trials?

Dataset

Dataset: CMU Keystroke Dynamics Benchmark
Source: Carnegie Mellon University
Format: CSV

The benchmark contains 20,400 records from 51 participants. Each participant completed 400 repetitions of a fixed password across eight sessions, with 50 repetitions per session.

The dataset includes participant identifiers, session information, repetition numbers, and 31 keystroke timing features.

Features Used
Feature	Description
subject	Participant identifier
sessionIndex	Session number
rep	Repetition number within a session
H.period	Hold duration of the period (.) key
Dataset Setup

The dataset is not included in this repository. Download the CSV from the official CMU source and place it in the data/ directory with the following filename:

DSL-StrongPasswordData.csv

The expected path is:

text
data/DSL-StrongPasswordData.csv


Please consult the original dataset source for attribution requirements and reuse or redistribution terms.

Methodology
1. Data Preparation

The dataset is loaded using Pandas. The analysis inspects the data structure and selects observations for one participant and session.

The selected configuration is:

Participant: s002
Session: 1
Feature: H.period
Observations: 50
Repetition range: 1–50

The observations are sorted by repetition number to preserve their trial order. Missing values in the selected feature are checked before analysis.

2. Time-Domain Analysis

Time-domain analysis summarizes the distribution and variation of key hold durations across the 50 repetitions.

The following descriptive statistics are calculated:

Number of observations
Mean
Standard deviation
Minimum
Maximum
Median

A line plot is generated to visualize hold duration against repetition number. A horizontal dashed line indicates the mean hold duration.

The resulting figure is saved as:

outputs/time_domain_H_period.png

3. Frequency-Domain Analysis Using FFT

The frequency-domain analysis investigates variation in the ordered sequence of hold durations.

The following steps are performed:

Remove the linear trend from the sequence using SciPy's detrend function.
Apply a Hann window to reduce spectral leakage.
Compute the one-sided FFT using rfft.
Calculate the corresponding frequency bins using rfftfreq.
Estimate the one-sided amplitude spectrum.
Identify the strongest nonzero frequency component.
Calculate the approximate repetition period associated with that frequency.
Plot the amplitude spectrum and mark the dominant component.

The resulting figure is saved as:

outputs/fft_H_period.png

Important interpretation note: The sequence is ordered by password repetition rather than sampled at uniform intervals of continuous time. Therefore, FFT frequencies are expressed in cycles per repetition, not hertz. Spectral peaks describe variation across trial order and do not establish a continuous typing rhythm.

Results

The analysis produced the following results for participant s002, session 1, using the H.period feature.

Time-Domain Results
Measure	Result
Number of observations	50
Mean hold duration	0.111288 s
Standard deviation (sample)	0.015222 s
Minimum hold duration	0.077600 s
Maximum hold duration	0.149100 s
Median hold duration	0.111800 s

The mean hold duration was approximately 111.3 milliseconds. The sample standard deviation was approximately 15.2 milliseconds, indicating variation in hold durations across the selected repetitions.

Frequency-Domain Results
Measure	Result
Number of observations	50
Frequency resolution	0.0200 cycles/repetition
Dominant nonzero frequency	0.3600 cycles/repetition
Approximate spectral period	2.78 repetitions
Peak amplitude	0.008922 s (approximate)

The strongest nonzero FFT component occurred at 0.36 cycles per repetition, corresponding to an approximate period of 2.78 repetitions.

This result is exploratory. The sequence contains only 50 observations, and the detected peak does not demonstrate a stable or recurring typing behavior. Further analysis across participants, sessions, and preprocessing methods would be needed to investigate the consistency of spectral patterns.

Visualizations

The notebook generates two figures.

1. Time-Domain Plot

File: outputs/time_domain_H_period.png

This plot displays the period-key hold duration for each repetition. The dashed horizontal line represents the mean hold duration.

It helps visualize changes, variability, and unusually high or low measurements across the selected trials.

2. Frequency-Domain Plot

File: outputs/fft_H_period.png

This plot displays the one-sided FFT amplitude spectrum after linear detrending and Hann windowing.

The dominant nonzero frequency is highlighted with a vertical dashed line. The horizontal axis represents cycles per repetition, not cycles per second.

Project Structure
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


Directory descriptions:

data/ — Contains the locally downloaded dataset.
notebooks/ — Contains the Jupyter Notebook used for the analysis.
outputs/ — Stores the generated visualization files.
src/ — Contains supporting Python scripts for data inspection.
requirements.txt — Lists the Python dependencies.
README.md — Documents the project, methodology, results, and setup instructions.

The dataset should not be committed to version control unless its redistribution terms have been verified. Consider adding the dataset path to .gitignore.

Requirements
Python 3.12 or a compatible Python version
Pandas
NumPy
Matplotlib
SciPy
Jupyter Notebook
IPython kernel (ipykernel)
Installation and Setup
Step 1: Obtain the Project and Dataset

Download or clone the project repository.

Obtain the CMU Keystroke Dynamics Benchmark separately from its official source and place the CSV file in the data/ directory.

Ensure that the filename is exactly:

text
DSL-StrongPasswordData.csv

Step 2: Open the Project Directory

On Windows, open Command Prompt (CMD) and navigate to the project directory:

cmd
cd /d "C:\HCI LAB\Keyboard_interaction"


Replace the path with your actual project location if necessary.

Step 3: Install Dependencies

Run the following command:

cmd
python -m pip install -r requirements.txt


If the requirements file has not yet been created, it can contain:

text
pandas
numpy
matplotlib
scipy
jupyter
ipykernel

Step 4: Launch Jupyter Notebook

Run:

cmd
python -m jupyter notebook


Alternatively, use:

cmd
jupyter notebook

Step 5: Run the Analysis

Open the following notebook in Jupyter:

text
notebooks/time_series_analysis.ipynb


Run the notebook cells from top to bottom.

The notebook will:

Load and inspect the dataset.
Select participant s002, session 1.
Extract the H.period feature.
Calculate descriptive statistics.
Generate and save the time-domain plot.
Perform detrending, windowing, and FFT analysis.
Generate and save the frequency-domain plot.
Print a summary of the results and verify the output files.

Make sure the dataset exists at the expected path before running the notebook.

Interpretation and Limitations

This project demonstrates basic time-series analysis techniques, but its findings must be interpreted within the limits of the dataset and methodology.

Limited sample: The detailed analysis covers one participant, one session, and 50 repetitions.
Limited generalizability: The findings cannot be generalized to all participants or keyboard interactions.
Trial-order sampling: Repetition order is not equivalent to continuous-time sampling. FFT frequencies therefore represent cycles per repetition rather than hertz.
Exploratory spectral peak: The dominant FFT component does not prove the existence of a stable behavioral cycle.
Preprocessing sensitivity: Results may vary with the selected feature, participant, session, detrending procedure, and windowing method.
No authentication evaluation: The project does not implement or evaluate a keystroke-based authentication system.
Dataset dependency: Results depend on the availability and integrity of the original CSV dataset.

The analysis should be treated as an educational demonstration of time-domain and frequency-domain methods rather than a validated behavioral model.

Future Improvements

Possible extensions include:

Compare multiple sessions for the same participant.
Analyze several participants to investigate between-person variability.
Examine additional hold-time and digraph timing features.
Compare distributions using histograms, box plots, and other descriptive visualizations.
Investigate spectral stability across longer sequences.
Compare different detrending and windowing procedures.
Evaluate the sensitivity of dominant-frequency estimates to preprocessing choices.
Automate the analysis for multiple participants and sessions.
Add unit tests and data-validation checks to improve reproducibility.
Attribution

Dataset: CMU Keystroke Dynamics Benchmark, developed for research into keystroke dynamics.

This project uses the benchmark for an educational analysis of keyboard timing measurements through descriptive statistics, visualization, and FFT.

It is not a reproduction of the benchmark's original anomaly-detection evaluation.

Please consult the original dataset documentation for the appropriate citation, attribution, and reuse terms.

License

The license for this project's analysis code has not yet been specified.

Dataset reuse and redistribution are subject to the original dataset's terms. The code and dataset should not be assumed to share the same license.

Author's Note

This project was developed as a small Human-Computer Interaction lab exercise to explore how statistical summaries and frequency-domain techniques can be applied to keyboard interaction measurements using Python.

The main objective is to understand the analysis workflow, visualize the results, and interpret the limitations of applying FFT to repetition-ordered keystroke data.
