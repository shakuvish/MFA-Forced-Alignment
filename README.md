\# Montreal Forced Aligner - Assignment



\## Project Overview

This project demonstrates forced alignment of speech audio with text transcriptions using the Montreal Forced Aligner (MFA), including handling of Out-of-Vocabulary (OOV) words.



\## Dataset

\- \*\*Audio files:\*\* 6 WAV files (3 from F2BJRLP dataset, 3 from ISLE dataset)

\- \*\*Transcripts:\*\* Corresponding text transcriptions

\- \*\*Total duration:\*\* 97.16 seconds



\## Installation \& Setup



\### Prerequisites

\- Windows 10/11

\- Miniconda3



\### Step 1: Install Miniconda

1\. Download from https://docs.conda.io/en/latest/miniconda.html

2\. Install with default settings

3\. Restart terminal



\### Step 2: Install Montreal Forced Aligner

```bash

\# Create conda environment

conda create -n aligner -c conda-forge montreal-forced-aligner



\# Activate environment

conda activate aligner



\# Verify installation

mfa version

```



\### Step 3: Download Models

```bash

\# Download acoustic model

mfa model download acoustic english\_us\_arpa



\# Download dictionary

mfa model download dictionary english\_us\_arpa



\# Download G2P model (for OOV handling)

mfa model download g2p english\_us\_arpa

```



\## Project Structure

```

MFA-Forced-Alignment-Assignment/

├── audio/                      # Audio files (.wav)

├── transcripts/                # Text transcriptions (.txt)

├── output\_before\_oov/          # TextGrids before OOV handling

├── output\_after\_oov/           # TextGrids after OOV handling

├── dictionary/                 # Custom pronunciation dictionary

├── screenshots/                # Praat visualization screenshots

├── docs/                       # Documentation

├── README.md                   # This file

└── REPORT.md                   # Detailed analysis report

```



\## Usage



\### Step 1: Prepare Data

Organize files with matching names:

```

corpus/

├── filename1.wav

├── filename1.txt

├── filename2.wav

├── filename2.txt

...

```



\### Step 2: Run Initial Alignment

```bash

mfa align corpus english\_us\_arpa english\_us\_arpa output --clean

```



\### Step 3: Validate \& Identify OOV Words

```bash

mfa validate corpus english\_us\_arpa english\_us\_arpa --ignore\_acoustics

```



\### Step 4: Handle OOV Words

Create custom dictionary with pronunciations for OOV words, then:

```bash

mfa align corpus english\_us\_arpa english\_us\_arpa output\_with\_oov --clean --custom\_mapping\_path custom\_dict.txt

```



\## Results

\- Initial alignment: 6 TextGrid files generated

\- OOV words identified: 22 word types (48 tokens)

\- Custom dictionary created with phonetic pronunciations

\- Re-alignment completed with custom dictionary



\## Visualization

TextGrid files can be opened in Praat for visualization:

1\. Download Praat: https://www.fon.hum.uva.nl/praat/

2\. Open TextGrid file + corresponding WAV file

3\. Select both → View \& Edit



\## Key Observations

\- See `REPORT.md` for detailed analysis

\- Comparison of before/after OOV handling

\- Alignment quality metrics



\## Author

\[Your Name]



\## Date

February 2026



\## License

Educational project for academic purposes

