# SC4015 Side-Channel Analysis (CPA on AES)

This project demonstrates a Correlation Power Analysis (CPA) attack to recover a 16-byte AES key from power traces.

The implementation is in a single script:
- `cpa_implementation.py`

It reads plaintext and waveform data from:
- `waveform.csv`

## Overview

The script performs the standard first-order CPA workflow:

1. Load plaintexts and power traces from CSV.
2. Use the first 100 traces for analysis (assignment requirement in code).
3. For each key-byte position (0 to 15):
	 - Build a hypothetical leakage model using:
		 - AES S-box output: `Sbox[plaintext_byte XOR key_guess]`
		 - Hamming weight leakage assumption
	 - Compute Pearson correlation between hypothetical leakage and each time sample.
	 - Pick the key guess with highest absolute correlation.
4. Print recovered key bytes.
5. Plot the key-byte-0 correlation profile.

## Requirements

- Python 3.9+
- `numpy`
- `scipy`
- `matplotlib`

Install dependencies:

```bash
pip install numpy scipy matplotlib
```

## Dataset Format

`waveform.csv` is expected to be comma-separated with this layout per row:

1. Plaintext (32 hex chars, 16 bytes)
2. Ciphertext (32 hex chars, currently not used by the script)
3. Power trace samples (floating-point values)

Example row structure:

```text
<plaintext_hex>,<ciphertext_hex>,<sample_0>,<sample_1>,...,<sample_n>
```

## How To Run

From the project root:

```bash
python -u cpa_implementation.py
```

## Expected Output

The script prints:

- Number of traces loaded and trace length
- Best key guess and correlation score for each byte
- Final recovered 16-byte key as hex list

It also opens a plot titled:
- `CPA Correlation for Key Byte 0`

## Project Files

- `cpa_implementation.py`: main CPA implementation
- `waveform.csv`: input traces and text data
- `README.md`: project documentation

## Notes

- The script currently slices to the first 100 traces (`NUM_TRACES = 100`).
- Correlation uses absolute Pearson values to score key hypotheses.
- The plot is generated only for byte 0 scores (`scores_byte0`).

## Possible Improvements

- Add command-line arguments for:
	- number of traces
	- input file path
	- optional output save path for figures
- Save recovered key and scores to a results file.
- Add a `requirements.txt` for one-command setup.

