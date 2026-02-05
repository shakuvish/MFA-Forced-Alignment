\# Installation Guide - Step by Step



\## For Windows Users



\### 1. Install Miniconda

```bash

\# Download from: https://docs.conda.io/en/latest/miniconda.html

\# Choose: Miniconda3 Windows 64-bit

\# Run installer with default settings

```



\### 2. Create MFA Environment

```bash

\# Open Command Prompt or Anaconda Prompt

conda create -n aligner -c conda-forge montreal-forced-aligner

conda activate aligner

```



\### 3. Verify Installation

```bash

mfa version

\# Should display version number (e.g., 3.x.x)

```



\### 4. Download Required Models

```bash

mfa model download acoustic english\_us\_arpa

mfa model download dictionary english\_us\_arpa

mfa model download g2p english\_us\_arpa

```



\### 5. Verify Models

```bash

mfa model list acoustic

mfa model list dictionary

mfa model list g2p

```



\## Running the Alignment



\### Prepare Your Data

1\. Create a folder called `corpus`

2\. Place audio files (.wav) and matching transcript files (.txt) in the same folder

3\. Ensure filenames match (e.g., `file1.wav` + `file1.txt`)



\### Run Alignment

```bash

\# Basic alignment

mfa align corpus english\_us\_arpa english\_us\_arpa output --clean



\# With custom dictionary for OOV words

mfa align corpus english\_us\_arpa english\_us\_arpa output --clean --custom\_mapping\_path custom\_dict.txt

```



\### Validate Corpus

```bash

mfa validate corpus english\_us\_arpa english\_us\_arpa --ignore\_acoustics

```



\## Install Praat for Visualization

1\. Download: https://www.fon.hum.uva.nl/praat/

2\. Extract and run `praat.exe`

3\. Open TextGrid + WAV files together to visualize alignment



\## Troubleshooting



\### Issue: Permission Denied Error

\- \*\*Solution:\*\* Move files to a simple path like `C:\\MFA\_Project` (avoid OneDrive/network drives)



\### Issue: File Extension Problems

\- \*\*Solution:\*\* Ensure all .txt files have lowercase extensions (not .TXT)



\### Issue: Empty G2P Output

\- \*\*Solution:\*\* Manually create custom dictionary using ARPA phonetic notation



\### Issue: "Command not found"

\- \*\*Solution:\*\* Make sure conda environment is activated: `conda activate aligner`



\## Resources

\- MFA Documentation: https://montreal-forced-aligner.readthedocs.io/

\- GitHub Repository: https://github.com/shakuvish/MFA-Forced-Alignment

