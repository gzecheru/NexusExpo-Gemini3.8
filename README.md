# Google GenAI Project Setup

This project demonstrates how to use the Google GenAI Python SDK (`google-genai`) with Gemini models.

---

## 1. Prerequisites & Virtual Environment

A Python virtual environment is already created in `.venv`.

To activate the virtual environment:

```bash
source .venv/bin/activate
```

If you ever need to recreate or reinstall the dependencies:

```bash
python3 -m venv .venv
source .venv/bin/activate
pip install google-genai python-dotenv
```

---

## 2. API Key Configuration

Ensure your API key is configured in `gemini.env`:

```env
GEMINI_API_KEY=your_gemini_api_key_here
```

---

## 3. Running the Code

Run the example script:

```bash
python example.py
```

Or run directly without manual activation:

```bash
.venv/bin/python example.py
```

---

## 4. Code Example

```python
import os
from dotenv import load_dotenv
from google import genai

# Load API key from gemini.env
load_dotenv("gemini.env")

# Initialize client
client = genai.Client(api_key=os.getenv("GEMINI_API_KEY"))

# Generate content
response = client.models.generate_content(
    model="gemini-2.5-flash",
    contents="Write a three.js script that renders a realistic 3D black hole."
)

print(response.text)
```
