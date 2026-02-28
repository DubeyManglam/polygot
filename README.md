# 🌍 Polygot CLI

Command-line interface for extracting and translating UI strings.

---

## 📦 Installation

### Global Installation
```bash
npm install -g polygot
```

### Local Installation
```bash
npm install polygot
npx polygot --help
```

---

# 🚀 Commands

---

## 🔍 Extract Strings

Extract UI strings from source files **without translation**:

```bash
polygot extract <source> <language> <output> [options]
```

### Arguments

- `source` – Source file or directory path  
- `language` – Source language code (e.g., en, es, fr)  
- `output` – Output directory for JSON files  

### Options

- `-a, --attributes <attrs>` – Comma-separated attributes (default: title,alt,placeholder)  
- `--no-progress` – Disable progress logging  

### Examples

```bash
# Extract from single file
polygot extract ./src/App.tsx en ./locales

# Extract from directory
polygot extract ./src en ./public/locales

# Extract with custom attributes
polygot extract ./src en ./locales --attributes "title,placeholder,aria*,data-*"

# Extract without progress
polygot extract ./src en ./locales --no-progress
```

---

## 🌎 Translate Strings

Extract and translate strings to target language(s):

```bash
polygot translate <source> <languages> <output> [options]
```

### Arguments

- `source` – Source file or directory path  
- `languages` – Target language codes (comma-separated)  
- `output` – Output directory for JSON files  

### Options

- `-k, --api-key <key>` – OpenAI API key  
- `-m, --model <model>` – OpenAI model (default: gpt-4o-mini)  
- `-c, --context <context>` – Translation context  
- `-t, --tone <tone>` – Translation tone: formal, casual, neutral (default: neutral)  
- `-a, --attributes <attrs>` – Attributes to extract (default: title,alt,placeholder,aria*)  
- `--chunk-size <size>` – Max strings per API call (default: 50)  
- `--no-formatting` – Don't preserve placeholders  
- `--no-progress` – Disable progress logging  

### Examples

```bash
# Basic translation
polygot translate ./src es ./locales --api-key sk-...

# Multiple languages
polygot translate ./src es,fr,de ./locales --api-key sk-...

# Using environment variable
export OPENAI_API_KEY=sk-...
polygot translate ./src es,fr,de ./locales

# With context and tone
polygot translate ./src es,fr ./locales \
  --api-key sk-... \
  --context "E-commerce website" \
  --tone casual

# Custom model & chunk size
polygot translate ./src es ./locales \
  --model gpt-4 \
  --chunk-size 30
```

---

## ⚙️ Initialize Config

Create a configuration file:

```bash
polygot init
```

Creates `polygot.config.json`:

```json
{
  "source": "./src",
  "output": "./public/locales",
  "languages": ["es", "fr", "de"],
  "attributes": ["title", "alt", "placeholder", "aria*"],
  "model": "gpt-4o-mini",
  "context": "Web application UI",
  "tone": "neutral",
  "chunkSize": 50
}
```

---

## 🔁 Translate Using Config

```bash
polygot translate-config
```

### Options

- `-c, --config <path>` – Custom config file path  
- `-k, --api-key <key>` – Override API key  

Example:

```bash
export OPENAI_API_KEY=sk-...
polygot translate-config
```

---

## 🌐 List Supported Languages

```bash
polygot languages
```

---

# 🧩 Workflow Examples

---

## Quick Start

```bash
polygot extract ./src en ./locales
export OPENAI_API_KEY=sk-...
polygot translate ./src es,fr ./locales
```

---

## Using Config File

```bash
polygot init
export OPENAI_API_KEY=sk-...
polygot translate-config
```

---

## CI/CD Example

```bash
#!/bin/bash
set -e

echo "Extracting strings..."
polygot extract ./src en ./public/locales

echo "Translating..."
polygot translate ./src es,fr,de \
  --api-key $OPENAI_API_KEY \
  --context "SaaS application" \
  --tone professional \
  --no-progress

echo "Done!"
```

---

# 🔐 Environment Variables

- `OPENAI_API_KEY` – Required for translation

---

# 💡 Tips

- Never commit your API key.
- Use `--chunk-size` to control API cost.
- Provide good `--context` for better translations.
- Use wildcard attributes like `aria*`, `data-*`.

---

# 🛠 Troubleshooting

### Command not found
```bash
npm link
```

### API key errors
```bash
export OPENAI_API_KEY=your_key
```

### Permission errors
```bash
chmod +x cli/polygot.js
chmod +x cli/index.js
```

---
