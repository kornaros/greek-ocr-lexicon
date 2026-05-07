# greek-ocr-lexicon
A JSON database of Greek words categorized by prefix for fast lookup.
# Greek Polytonic OCR Lexicon

This repository hosts a specialized morphological dictionary (`lexicon.json`) designed to enhance the accuracy of Optical Character Recognition (OCR) for Ancient and Modern Greek polytonic texts.

## 📖 Project Overview
The dictionary is structured to support real-time text correction by mapping OCR-generated strings to their correct polytonic forms. It uses a prefix-based organization (based on the first two letters of each word) to ensure high-performance lookups in web environments.

### Key Features:
*   **Polytonic Support**: Includes breathings, accents, and iota subscripts[cite: 2].
*   **OCR-Resilient**: Optimized to handle common character recognition errors (e.g., confusing κ, χ, and λ)[cite: 2].
*   **Web-Ready**: Specifically formatted for easy integration with JavaScript `fetch` calls in HTML/Web applications.

## 🛠 File Structure
The `lexicon.json` file is organized by prefixes. Each entry contains:
*   The "clean" version (lowercase, no accents/spirits) for matching.
*    The "original" polytonic version for the final correction.

Example:
```json
"βι": [
  {
     "βιβλιο",
    "βιβλίο"
  }
]
```

## 🔄 How to Update the Lexicon

To add new words or clean duplicates, use the following Python logic in your local Jupyter Notebook (.ipynb):

```python
import json
import unicodedata

def remove_accents(input_str):
    nfkd_form = unicodedata.normalize('NFKD', input_str)
    return "".join([c for c in nfkd_form if not unicodedata.combining(c)]).lower()

# To add new words:
new_words = ["παράδειγμα", "λόγος"]
# Load your local lexicon.json, append entries, and save.
```

## 🚀 Integration with HTML
To use this lexicon in your OCR tool, use the Raw URL from GitHub in your script

```JavaScript
const GITHUB_LEXICON_URL = "[https://raw.githubusercontent.com/](https://raw.githubusercontent.com/)[YOUR_USERNAME]/[YOUR_REPO]/main/lexicon.json";

async function autoLoadLexicon() {
    const response = await fetch(GITHUB_LEXICON_URL);
    const data = await response.json();
    // Process and enable the dictionary buttons
}
```

## ⚖️ License
This project is licensed under the [MIT License](LICENSE)

