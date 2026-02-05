# Montreal Forced Aligner - Assignment

## Project Overview
This project demonstrates forced alignment of speech audio with text transcriptions using the Montreal Forced Aligner (MFA), including handling of Out-of-Vocabulary (OOV) words.

## Dataset
- Audio files: 6 WAV files (3 from F2BJRLP dataset, 3 from ISLE dataset)
- Transcripts: Corresponding text transcriptions
- Total duration: 97.16 seconds

## Installation & Setup

### Prerequisites
- Windows 10/11
- Miniconda3

### Step 1: Install Miniconda
1. Download from https://docs.conda.io/en/latest/miniconda.html
2. Install with default settings
3. Restart terminal

### Step 2: Install Montreal Forced Aligner
```bash
# Create conda environment
conda create -n aligner -c conda-forge montreal-forced-aligner
# Activate environment
conda activate aligner
# Verify installation
mfa version
```

### Step 3: Download Models
```bash
# Download acoustic model
mfa model download acoustic english_us_arpa
# Download dictionary
mfa model download dictionary english_us_arpa
# Download G2P model (for OOV handling)
mfa model download g2p english_us_arpa
```

## Project Structure
```
MFA-Forced-Alignment-Assignment/
├── audio/                  # Original .wav files
├── transcripts/            # Original .txt transcription files
├── corpus/                 # Paired audio + text files (created during usage)
├── dictionary/             # Custom pronunciation dictionary files
├── output_before_oov/      # TextGrid files (initial alignment)
├── output_after_oov/       # TextGrid files (after OOV handling)
├── screenshots/            # Praat visualization screenshots
├── docs/                   # Additional documentation
├── REPORT.md               # Detailed analysis and observations
└── README.md               # This file
```

## Usage

### Step 1: Prepare the Corpus Directory
MFA requires audio and transcription files to share the same base name in a single directory.

```bash
mkdir corpus
cp audio/*.wav corpus/
cp transcripts/*.txt corpus/
```

### Step 2: Initial Alignment
```bash
mfa align corpus/ english_us_arpa english_us_arpa output_before_oov/ --clean
```

### Step 3: Validate & Identify OOV Words
```bash
mfa validate corpus/ english_us_arpa english_us_arpa --ignore_acoustics
```
This command produces logs including oovs_found.txt with all OOV words and their counts.

### Step 4: Handle OOV Words with Custom Dictionary
1. Save the base dictionary locally:
   ```bash
   mfa model save dictionary english_us_arpa dictionary/base_dict.txt
   ```

2. Create custom dictionary:
   ```bash
   cp dictionary/base_dict.txt dictionary/custom_dict.txt
   ```
   Edit custom_dict.txt and add manual pronunciations for OOV words in ARPABET format.

3. Re-run alignment with custom dictionary:
   ```bash
   mfa align corpus/ dictionary/custom_dict.txt english_us_arpa output_after_oov/ --clean
   ```

## Results
- Initial alignment: 6 TextGrid files generated in output_before_oov/
- OOV words identified: 22 unique types (48 total tokens)
- Custom dictionary created with phonetic pronunciations for all OOV items
- Final alignment completed with improved TextGrids in output_after_oov/

## Visualization
TextGrid files can be opened in Praat for visualization:
1. Download Praat: https://www.fon.hum.uva.nl/praat/
2. Open the corresponding .wav file and .TextGrid file
3. Select both objects and click View & Edit

Screenshots of before/after OOV handling comparisons are stored in the screenshots/ folder.

## Key Observations
- Alignment accuracy improved significantly after adding custom pronunciations
- Most OOV issues were caused by proper names and non-standard terms
- Detailed analysis and metrics are provided in REPORT.md

## Author
Shashank Vishwakarma

## Date
February 2026
