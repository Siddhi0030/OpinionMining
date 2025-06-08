# Transliterated Marathi Sentiment Analysis

A comprehensive sentiment analysis system for transliterated Marathi text using machine learning techniques. The project combines lexicon-based scoring with Support Vector Machine (SVM) classification to provide accurate sentiment predictions for both individual sentences and complete paragraphs.

## 🌟 Features

- **Dual Analysis Modes**: Analyze single sentences or complete paragraphs
- **Lexicon-Based Scoring**: Uses custom Marathi sentiment lexicon for initial scoring
- **SVM Classification**: Machine learning model trained on processed data for accurate predictions
- **7-Point Sentiment Scale**: From "Most Negative" (-3) to "Most Positive" (+3)
- **REST API**: FastAPI-based backend with multiple endpoints
- **Modern UI**: React-based frontend with real-time analysis

## 🏗️ Project Structure

```
project/
├── backend/
│   ├── sentiment_logic.py      # Core sentiment analysis logic
│   └── main.py                 # FastAPI application
├── data/
│   ├── Senti_Words.csv         # Marathi sentiment lexicon
│   └── Data.csv               # Training dataset
├── frontend/
│   └── src/
│       └── SentimentForm.jsx   # React frontend component
├── README.md
└── requirements.txt            # Dependencies file
```

## 🚀 Quick Start

### Prerequisites

- Python 3.10+
- Node.js 16+
- npm or yarn

### Backend Setup

1. **Clone the repository**
   ```bash
   git clone https://github.com/Siddhi0030/OpinionMining.git
   cd OpinionMining
   ```

2. **Install Python dependencies**
   ```bash
   cd backend
   pip install -r requirements.txt
   ```

3. **Start the API server**
   ```bash
   python main.py
   ```
   The API will be available at `http://localhost:8000`

### Frontend Setup

1. **Navigate to UI directory**
   ```bash
   cd frontend
   ```

2. **Install dependencies**
   ```bash
   npm install
   # or
   yarn install
   ```

3. **Start the development server**
   ```bash
   npm start
   # or
   yarn start
   ```
   The frontend will be available at `http://localhost:3000`

## 📚 API Documentation

### Endpoints

#### `POST /analyze_sentence`
Analyze a single sentence
```json
{
  "text": "mi khup khush aahe"
}
```

**Response:**
```json
{
  "text": "mi khup khush aahe",
  "score": 2,
  "label": "More Positive",
  "cleaned_text": "mi khup khush aahe"
}
```

#### `POST /analyze_paragraph`
Analyze a complete paragraph
```json
{
  "paragraph": "mi khup khush aahe. pan aaj thoda sad aahe."
}
```

**Response:**
```json
{
  "paragraph": "mi khup khush aahe. pan aaj thoda sad aahe.",
  "average_score": 0.5,
  "average_label": "Neutral",
  "sentence_details": ["More Positive [2]", "Negative [-1]"]
}
```

### Interactive API Documentation

Visit `http://localhost:8000/docs` for Swagger UI documentation or `http://localhost:8000/redoc` for ReDoc documentation.

## 🎯 Sentiment Categories

| Score | Label | Description |
|-------|-------|-------------|
| +3 | Most Positive | Extremely positive sentiment |
| +2 | More Positive | Very positive sentiment |
| +1 | Positive | Positive sentiment |
| 0 | Neutral | Neutral sentiment |
| -1 | Negative | Negative sentiment |
| -2 | More Negative | Very negative sentiment |
| -3 | Most Negative | Extremely negative sentiment |

## 🔧 Technical Details

### Algorithm Overview

1. **Text Preprocessing**: 
   - Convert to lowercase
   - Remove special characters
   - Normalize whitespace

2. **Lexicon-Based Scoring**:
   - Match words against Marathi sentiment lexicon
   - Calculate cumulative sentiment score

3. **Score Normalization**:
   - Normalize scores to -3 to +3 range
   - Apply classification thresholds

4. **SVM Classification**:
   - Bag-of-Words vectorization
   - Linear SVM for final prediction

### Model Performance

- **Vectorization**: CountVectorizer (Bag-of-Words)
- **Classifier**: Support Vector Machine with linear kernel
- **Training Split**: 80% training, 20% testing
- **Features**: Word-level tokens from preprocessed text

## 📊 Usage Examples

### Python Backend Usage

```python
from sentiment_logic import MarathiSentimentAnalyzer

# Initialize and train
analyzer = MarathiSentimentAnalyzer()
analyzer.train_model()

# Analyze single sentence
score, label, cleaned = analyzer.analyze_sentence("mi khup khush aahe")
print(f"Sentiment: {label} (Score: {score})")

# Analyze paragraph
avg_score, avg_label, details = analyzer.analyze_paragraph(
    "mi khup khush aahe. pan aaj thoda sad aahe."
)
print(f"Overall: {avg_label} (Average Score: {avg_score})")
```

## 🛠️ Development

### Adding New Features

1. **Backend**: Extend the `MarathiSentimentAnalyzer` class in `sentiment_logic.py`
2. **API**: Add new endpoints in `main.py`
3. **Frontend**: Update `SentimentForm.jsx` for UI changes

### Custom Lexicon

To use your own sentiment lexicon:
1. Replace `data/Senti_Words.csv` with your lexicon file
2. Ensure it has columns: `Word`, `Score`
3. Restart the backend server

### Model Retraining

The model automatically trains on startup. To retrain:
1. Update `data/Data.csv` with new training samples
2. Restart the backend server

---

**Note**: This system is designed for transliterated Marathi text (Marathi written in English/Latin script). For native Devanagari script analysis, additional preprocessing may be required.
