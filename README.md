# LinkedIn Post Generator

An AI-powered application that generates LinkedIn posts using few-shot learning and LLMs. This tool leverages language models to create engaging LinkedIn content based on specified topics, lengths, and languages.

## Overview

The LinkedIn Post Generator is a Python-based application that uses advanced language models to generate customized LinkedIn posts. It combines few-shot learning with LLM capabilities to produce high-quality, contextually relevant posts in multiple languages.

## Features

- **AI-Powered Generation**: Uses Groq's API with advanced language models to generate LinkedIn posts
- **Customizable Parameters**:
  - **Length**: Short (1-5 lines), Medium (6-10 lines), or Long (11-15 lines)
  - **Language**: English or Hinglish (Hindi + English mix)
  - **Topic/Tags**: Choose from various predefined topics
- **Few-Shot Learning**: Leverages example posts to maintain consistent writing style
- **Web Interface**: Interactive Streamlit-based UI for easy post generation
- **Tag Unification**: Automatically categorizes and unifies tags for better organization

## Project Structure

```
linkedin-post-generator/
├── main.py              # Streamlit web application
├── few_shot.py          # Few-shot post management and filtering
├── post_generator.py    # Core post generation logic
├── llm_helper.py        # LLM initialization and configuration
├── preprocess.py        # Data preprocessing and metadata extraction
├── data/                # Data directory
│   ├── raw_posts.json   # Raw LinkedIn posts (input)
│   └── processed_posts.json # Processed posts with metadata (output)
└── .gitignore          # Git ignore configuration
```

## Components

### `main.py`
The main Streamlit application that provides the user interface. Users can:
- Select a topic/tag
- Choose post length
- Select language preference
- Generate posts with a single click

### `few_shot.py`
Manages the few-shot examples used for prompt engineering:
- Loads preprocessed posts from JSON
- Categorizes posts by length
- Extracts unique tags
- Filters posts based on language, length, and tag

### `post_generator.py`
Handles the core post generation logic:
- Constructs intelligent prompts with few-shot examples
- Interfaces with the LLM to generate posts
- Returns generated content to the user

### `llm_helper.py`
Initializes and configures the language model:
- Sets up Groq API connection
- Configures the ChatGroq model with OpenAI-compatible models

### `preprocess.py`
Preprocesses raw LinkedIn post data:
- Extracts metadata from posts (line count, language, tags)
- Unifies and standardizes tags
- Enriches posts with extracted metadata
- Outputs processed data for use in few-shot learning

## Requirements

- Python 3.8+
- Dependencies:
  - `streamlit` - Web application framework
  - `pandas` - Data manipulation
  - `langchain-groq` - Groq LLM integration
  - `langchain-core` - LangChain core utilities
  - `python-dotenv` - Environment variable management

## Installation

1. **Clone the repository**:
   ```bash
   git clone https://github.com/ayah05/linkedin-post-generator.git
   cd linkedin-post-generator
   ```

2. **Create a virtual environment** (recommended):
   ```bash
   python -m venv venv
   source venv/bin/activate  # On Windows: venv\Scripts\activate
   ```

3. **Install dependencies**:
   ```bash
   pip install -r requirements.txt
   ```

4. **Set up environment variables**:
   Create a `.env` file in the project root:
   ```
   GROQ_API_KEY=your_groq_api_key_here
   ```

## Usage

### Option 1: Run with Streamlit UI

```bash
streamlit run main.py
```

Then open your browser and navigate to `http://localhost:8501`

### Option 2: Data Preprocessing

To preprocess raw posts before generating:

```bash
python preprocess.py
```

This will:
- Read from `data/raw_posts.json`
- Extract metadata from each post
- Unify tags using the LLM
- Output processed posts to `data/processed_posts.json`

### Option 3: Direct Python Usage

```python
from post_generator import generate_post

# Generate a post
post = generate_post(length="Short", language="English", tag="Job Search")
print(post)
```

## Data Format

### Raw Posts (data/raw_posts.json)
```json
[
  {
    "text": "Your LinkedIn post text here...",
    "tags": ["tag1", "tag2"]
  },
  ...
]
```

### Processed Posts (data/processed_posts.json)
```json
[
  {
    "text": "Your LinkedIn post text here...",
    "tags": ["unified_tag"],
    "line_count": 5,
    "language": "English",
    "length": "Short"
  },
  ...
]
```

## How It Works

1. **Input**: User selects topic, length, and language through the Streamlit interface
2. **Few-Shot Examples**: The system retrieves 1-2 example posts matching the criteria
3. **Prompt Engineering**: A detailed prompt is constructed with examples and specifications
4. **LLM Generation**: The Groq API processes the prompt using an advanced language model
5. **Output**: A customized LinkedIn post is generated and displayed to the user

## Technologies Used

- **LLM**: Groq API (OpenAI-compatible models)
- **Web Framework**: Streamlit
- **Data Processing**: Pandas
- **Language Chain**: LangChain
- **API Integration**: LangChain Groq

## Configuration

### Model Selection
The LLM model can be configured in `llm_helper.py`:
```python
llm = ChatGroq(
    groq_api_key=os.getenv("GROQ_API_KEY"), 
    model_name="openai/gpt-oss-120b"
)
```

### Post Length Thresholds
Modify length categorization in `few_shot.py` `categorize_length()` method.

## Future Enhancements

- Add support for more languages
- Implement user feedback mechanism to improve post quality
- Add post scheduling capabilities
- Support for image/media recommendations
- User authentication and history tracking
- Batch post generation
- A/B testing different prompt strategies

## License

This project is open source and available under the MIT License.

## Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

## Author

[ayah05](https://github.com/ayah05)

## Support

For issues or questions, please open an issue on the [GitHub repository](https://github.com/ayah05/linkedin-post-generator/issues).
