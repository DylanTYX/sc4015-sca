# SC4015 Side-Channel Analysis Project Submission

## What This Project Is
In this project, we implemented Correlation Power Analysis (CPA) on the provided measured power traces in waveform.csv to recover all 16 bytes of the AES key.

We based this implementation on the CPA workflow from lab (simulated traces) and extended it to work on the real waveform dataset.

## Group Members
We will fill in the final team details here before submission:

- Member 1: Full Name, Matriculation Number
- Member 2: Full Name, Matriculation Number
- Member 3: Full Name, Matriculation Number

## Submission Deadline
19 April 2026

## Files in This Submission
- cpa_implementation.py: Our CPA implementation
- waveform.csv: Input trace dataset used by the code
- README.md: This file (execution and project summary)

## What We Implemented
Our script does the following:

1. Reads plaintexts and power traces from waveform.csv.
2. Uses the first 100 traces for the assignment requirement.
3. For each AES key byte position (0 to 15):
   - Generates hypothetical leakage for all 256 key guesses using Hamming weight of S-box output.
   - Computes Pearson correlation between hypothetical leakage and measured traces across all time samples.
   - Takes the maximum absolute correlation for each key guess.
   - Selects the key guess with the highest score as the recovered byte.
4. Prints the recovered 16-byte key.
5. Produces Plot-1 for key byte 0 (all 256 key guesses), with the best guess highlighted in red.

## Environment and Dependencies
We used Python 3 with these packages:

```bash
pip install numpy scipy matplotlib
```

## How We Run the Code
From the project root:

```bash
python -u cpa_implementation.py
```

## Expected Output
When the script runs, it prints:

- Number of traces loaded and trace length
- Best key-byte guess and correlation score for each byte index
- Final recovered key (16 bytes in hex)

It also opens a plot for byte 0 correlation scores.

## Plot-1 (Used in Our Report)
For key byte K0, we:

1. Build a correlation matrix C of size 256 x 2500.
2. Take the maximum absolute correlation value from each row.
3. Plot these 256 values:
   - X-axis: key guess (0 to 255)
   - Y-axis: max absolute correlation
4. Mark the best (correct) key guess in red.

## Notes
This README is written to accompany our code submission and provide reproducible execution steps for grading.