Keyboard Interaction Time-Series Analysis

Time-Domain and Frequency-Domain (FFT) Analysis of Keystroke Timing Data

1. Project Overview

This project explores keyboard interaction measurements using descriptive statistics, time-series visualization, and the Fast Fourier Transform (FFT).

The analysis uses the Carnegie Mellon University (CMU) Keystroke Dynamics Benchmark to study variations in key hold duration across repeated typing trials.

The project focuses on two approaches:

Time-domain analysis: Calculates descriptive statistics such as mean, standard deviation, minimum, maximum, and median.
Frequency-domain analysis: Applies FFT to an ordered sequence of measurements to examine how variation is distributed across repetition-order frequencies.

This project is intended for educational purposes as part of a Human-Computer Interaction (HCI) lab exercise. It does not implement a keyboard-based authentication system.

2. Research Question

How can time-domain statistics and frequency-domain analysis characterize variation in a keyboard timing feature across repeated typing trials?

3. Dataset

Dataset: CMU Keystroke Dynamics Benchmark
Format: CSV

The dataset contains 20,400 records from 51 participants. Each participant completed 400 repetitions of a fixed password across eight sessions, with 50 repetitions per session.

Features Used
Feature	Description
subject	Participant identifier
sessionIndex	Session number
rep	Repetition number within a session
H.period	Hold duration of the period key
Dataset Setup

The dataset is not included in this repository. Download it from the official CMU source and place it in the data/ directory.

Expected file path:

text
data/DSL-StrongPasswordData.csv


Refer to the original dataset documentation for attribution and reuse requirements.

4. Methodology
4.1 Data Preparation

The dataset is loaded using Pandas. The analysis selects participant s002, session 1, and the H.period feature.

The observations are sorted by repetition number, and missing values are checked before analysis.

4.2 Time-Domain Analysis

The following descriptive statistics are calculated:

Number of observations
Mean hold duration
Standard deviation
Minimum and maximum hold duration
Median hold duration

A line plot visualizes hold duration across repetitions, with a horizontal line indicating the mean.

Output: outputs/time_domain_H_period.png

4.3 Frequency-Domain Analysis (FFT)

The frequency-domain analysis follows these steps:

Remove the linear trend using SciPy's detrending function.
Apply a Hann window to reduce spectral leakage.
Calculate the one-sided FFT using rfft.
Compute the corresponding frequency bins using rfftfreq.
Estimate the amplitude spectrum.
Identify the strongest nonzero frequency component.
Calculate its approximate period in repetitions.
Plot the amplitude spectrum and highlight the dominant frequency.

Output: outputs/fft_H_period.png

Note: The measurements are ordered by repetition number rather than sampled at uniform intervals of continuous time. Therefore, frequencies are expressed in cycles per repetition, not hertz. Spectral peaks indicate variation across trial order and do not establish a continuous typing rhythm.

5. Results

The analysis was performed on 50 observations from participant s002, session 1.

5.1 Time-Domain Results
Measure	Result
Number of observations	50
Mean hold duration	0.111288 s
Standard deviation	0.015222 s
Minimum hold duration	0.077600 s
Maximum hold duration	0.149100 s
Median hold duration	0.111800 s

The mean hold duration was approximately 111.3 milliseconds, with a standard deviation of approximately 15.2 milliseconds. These statistics summarize the central tendency and variation in hold duration across the selected repetitions.

5.2 Frequency-Domain Results
Measure	Result
Number of observations	50
Frequency resolution	0.0200 cycles/repetition
Dominant nonzero frequency	0.3600 cycles/repetition
Approximate spectral period	2.78 repetitions
Peak amplitude	0.008922 s (approximate)

The strongest nonzero FFT component occurred at 0.36 cycles per repetition, corresponding to an approximate period of 2.78 repetitions.

This is an exploratory result, not evidence of a stable periodic typing behavior. The short sequence and repetition-order sampling limit the conclusions that can be drawn from the spectrum.

6. Visualizations

The notebook generates two figures:

Time-Domain Plot

File: outputs/time_domain_H_period.png

Displays key hold duration against repetition number, with the mean hold duration indicated by a horizontal dashed line.

Frequency-Domain Plot

File: outputs/fft_H_period.png

Displays the one-sided FFT amplitude spectrum after detrending and Hann windowing. The dominant nonzero frequency is highlighted.

7. Project Structure
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

data/ — Stores the locally downloaded dataset.
notebooks/ — Contains the Jupyter Notebook.
outputs/ — Stores the generated plots.
src/ — Contains supporting Python scripts.
requirements.txt — Lists the project dependencies.

The dataset should not be committed to version control unless its redistribution terms have been verified.

8. Requirements
Python 3.12 or a compatible version
Pandas
NumPy
Matplotlib
SciPy
Jupyter Notebook
IPython kernel (ipykernel)
9. How to Run
Step 1: Open the Project Directory

Open Command Prompt and navigate to the project folder:

cmd
cd /d "C:\HCI LAB\Keyboard_interaction"

Step 2: Install Dependencies
cmd
python -m pip install -r requirements.txt


If requirements.txt has not been created, add the following dependencies:

text
pandas
numpy
matplotlib
scipy
jupyter
ipykernel

Step 3: Launch Jupyter Notebook
cmd
python -m jupyter notebook

Step 4: Run the Notebook

Open the following file in Jupyter Notebook:

text
notebooks/time_series_analysis.ipynb


Run all cells from top to bottom.

Ensure that data/DSL-StrongPasswordData.csv exists before running the notebook.

The notebook will load the dataset, calculate descriptive statistics, perform FFT analysis, generate both visualizations, and verify that the output files have been saved.

10. Limitations
The detailed analysis covers only one participant, one session, and 50 repetitions.
The findings cannot be generalized to all participants or keyboard interactions.
Repetition order is not equivalent to continuous-time sampling.
FFT frequencies represent cycles per repetition rather than hertz.
The dominant spectral component does not prove that a stable behavioral cycle exists.
Results may vary depending on the selected feature, participant, session, detrending procedure, and windowing method.
The project does not implement or evaluate a keystroke-based authentication system.

The findings should be interpreted as an educational demonstration of time-domain and frequency-domain analysis.

11. Future Improvements
Compare multiple sessions for the same participant.
Analyze timing features across multiple participants.
Examine additional hold-time and digraph timing features.
Compare distributions using histograms and box plots.
Investigate spectral stability across longer sequences.
Evaluate the effects of different detrending and windowing methods.
Automate the analysis for multiple participants and sessions.
12. Attribution

Dataset: CMU Keystroke Dynamics Benchmark.

The dataset was developed for research into keystroke dynamics. This project presents an educational analysis using descriptive statistics, visualization, and FFT.

It is not a reproduction of the benchmark's original anomaly-detection evaluation.

Please consult the original CMU dataset documentation for the appropriate citation, attribution, and reuse terms.

13. License

The license for the analysis code has not yet been specified. Dataset reuse and redistribution are subject to the original dataset's terms. The code and dataset should not be assumed to share the same license.
