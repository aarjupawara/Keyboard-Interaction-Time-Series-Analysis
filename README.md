Keyboard Interaction Time-Series Analysis

Time-Domain and Frequency-Domain (FFT) Analysis of Keystroke Timing Data

A small Human-Computer Interaction (HCI) lab project exploring keyboard interaction measurements using descriptive statistics, time-series visualization, and the Fast Fourier Transform (FFT).

Project Overview

This project analyzes keystroke timing measurements from the Carnegie Mellon University (CMU) Keystroke Dynamics Benchmark. It demonstrates two complementary approaches to time-series analysis:

Time-domain analysis: summarizes key hold durations using the mean, standard deviation, minimum, maximum, and median.
Frequency-domain analysis: applies the FFT to an ordered sequence of measurements to explore how variation is distributed across repetition-order frequencies.

The project is intended for educational use and reproducible analysis. It does not implement a keyboard-based authentication system.

Dataset

Source: CMU Keystroke Dynamics Benchmark

The benchmark contains 20,400 records from 51 participants. Each participant completed 400 repetitions of a fixed password across eight sessions, with 50 repetitions per session.

The dataset contains participant and session identifiers, repetition numbers, and 31 keystroke timing features.

The analysis uses the following fields:

Feature	Description
subject	Participant identifier
sessionIndex	Session number
rep	Repetition number within a session
H.period	Hold duration of the period key

Dataset availability: Download the CSV from the official CMU website and place it at data/DSL-StrongPasswordData.csv. The dataset is not included in this repository.

Please consult the original source for dataset attribution and reuse terms.

Research Question

How can time-domain statistics and frequency-domain analysis characterize variation in a keyboard timing feature across repeated typing trials?

Methodology
1. Data preparation
Load the CSV using pandas.
Inspect its dimensions, column names, data types, and missing values.
Select participant s002, session 1.
Sort the observations by repetition number.
Extract the H.period feature.
2. Time-domain analysis

Calculate the mean, standard deviation, minimum, maximum, and median of the 50 observations. Plot hold duration against repetition number and save the figure.

3. Frequency-domain analysis
Remove a linear trend from the selected sequence.
Apply a Hann window to reduce spectral leakage.
Calculate the one-sided FFT amplitude spectrum.
Identify the strongest nonzero frequency component.
Plot and save the spectrum.

Interpretation limitation: The observations are ordered by password repetition, not sampled at uniform time intervals. Therefore, FFT frequencies are expressed in cycles per repetition, not hertz. Spectral peaks describe variation across trial order and do not establish a continuous typing rhythm.

Results

For participant s002, session 1, the observed results were:

Measure	Result
Number of observations	50
Mean hold duration	0.111288 s
Standard deviation	0.015222 s
Minimum	0.077600 s
Maximum	0.149100 s
Median	0.111800 s
Dominant nonzero FFT component	0.36 cycles/repetition
Approximate spectral period	2.78 repetitions

The mean hold duration was approximately 111.3 milliseconds. The standard deviation indicates variation in hold duration across repetitions.

The strongest nonzero FFT component occurred at 0.36 cycles per repetition. Given the short sequence and the trial-order interpretation, this is an exploratory spectral result rather than evidence of a stable periodic typing behavior.

Visualizations

The notebook generates two figures:

outputs/time_domain_H_period.png — hold duration across repetitions with the mean indicated.
outputs/fft_H_period.png — one-sided FFT amplitude spectrum.
Project Structure
text
Keyboard_interaction/
├── data/
│   └── DSL-StrongPasswordData.csv
├── notebooks/
│   └── time_series_analysis.ipynb
├── outputs/
│   ├── time_domain_H_period.png
│   └── fft_H_period.png
├── src/
│   └── inspect_data.py
├── .gitignore
├── README.md
└── requirements.txt


The dataset is stored locally and should not be committed unless its redistribution terms have been verified.

Requirements
Python 3.12 or compatible Python version
pandas
NumPy
Matplotlib
SciPy
Jupyter
ipykernel
How to Run
1. Clone or download the repository

Download the project and obtain the dataset separately from the official CMU source.

2. Open CMD in the project directory
cmd
cd /d "C:\HCI LAB\Keyboard_interaction"

3. Install dependencies
cmd
python -m pip install -r requirements.txt

4. Launch Jupyter
cmd
python -m jupyter notebook


Open notebooks/time_series_analysis.ipynb and run the cells from top to bottom.

Ensure the dataset exists at data/DSL-StrongPasswordData.csv before running the notebook.

Limitations
The detailed analysis uses one participant, one session, and 50 repetitions.
The findings should not be generalized to all participants or all keyboard interactions.
The FFT assumes an ordered numerical sequence; repetition order is not equivalent to continuous time sampling.
The dominant spectral component does not prove that a stable behavioral cycle exists.
Results depend on the selected feature, participant, session, detrending procedure, and windowing method.
Attribution

Dataset: CMU Keystroke Dynamics Benchmark.

The dataset was developed for research into keystroke dynamics. This project uses an alternative educational analysis based on time-domain statistics and FFT. It is not a reproduction of the original benchmark's anomaly-detection evaluation.

Future Improvements
Compare multiple sessions for the same participant.
Examine additional hold-time and digraph timing features.
Compare the time-domain distributions of multiple participants.
Investigate the stability of spectral results across longer sequences and different preprocessing methods.
License

The license for this analysis code has not yet been specified. Dataset reuse and redistribution are subject to the original dataset's terms. Do not assume that the dataset itself is covered by the code's eventual license.