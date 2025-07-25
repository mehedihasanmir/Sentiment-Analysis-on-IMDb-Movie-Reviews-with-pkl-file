
# 🎬 Sentiment Analysis on IMDb Movie Reviews using Pickle Model

This project performs sentiment analysis on IMDb movie reviews using supervised machine learning techniques. The goal is to classify movie reviews as either positive or negative based on their textual content. The model is trained using various machine learning algorithms and the best-performing one is saved as a .pkl (pickle) file for future predictions.
---

## 📁 Project Structure

```
📦 Sentiment-Analysis-on-IMDb-Movie-Reviews-with-pkl-file
├── IMDB Dataset.csv              # Dataset of movie reviews and sentiments
├── moview-review.ipynb           # Jupyter notebook with all code steps
├── model.pkl                     # Trained and saved ML model
├── vectorizer.pkl                # Saved TF-IDF vectorizer
├── README.md                     # Documentation file (this file)
└── .ipynb_checkpoints/           # Notebook checkpoints (auto-generated)
```

---

## 📚 Technologies & Libraries Used

- `pandas`, `numpy` – Data manipulation
- `matplotlib`, `seaborn` – Data visualization
- `nltk` – Natural Language Processing (stopwords, stemming)
- `sklearn` – ML models, vectorization, evaluation
- `pickle` – Save/load model and vectorizer
- `re`, `warnings` – Regular expression for text cleaning, warning control

---

## 🔄 Step-by-Step Workflow

### 1. **Import Libraries**
All required libraries for data processing, visualization, and machine learning are imported.

### 2. **Load Dataset**
```python
df = pd.read_csv("IMDB Dataset.csv")
```
- The dataset contains two columns: `review` (text) and `sentiment` (positive/negative).

### 3. **Data Preprocessing**
Performed using `re`, `nltk`, and `sklearn`.

Steps include:
- Removing HTML tags, punctuations, and numbers
- Lowercasing text
- Removing stopwords using `nltk.corpus.stopwords`
- Stemming using `PorterStemmer`

### 4. **Feature Extraction with TF-IDF**
```python
from sklearn.feature_extraction.text import TfidfVectorizer

vectorizer = TfidfVectorizer(max_features=5000)
X = vectorizer.fit_transform(corpus).toarray()
```
Text data is converted into numerical features.

### 5. **Train-Test Split**
```python
from sklearn.model_selection import train_test_split

X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=42)
```

### 6. **Model Training**
Multiple ML models are trained:
- Logistic Regression
- Decision Tree
- Random Forest
- Gaussian Naive Bayes
- Support Vector Machine (SVM)

Each model is evaluated using:
- Accuracy Score
- Confusion Matrix
- Classification Report (Precision, Recall, F1)

### 7. **Model Evaluation**
```python
from sklearn.metrics import accuracy_score, classification_report, confusion_matrix
```
Best model is chosen based on highest accuracy and balanced precision-recall.

### 8. **Saving the Model & Vectorizer**
```python
import pickle

with open("model.pkl", "wb") as file:
    pickle.dump(best_model, file)

with open("vectorizer.pkl", "wb") as file:
    pickle.dump(vectorizer, file)
```

---

## 📌 How to Use This Project

### 🔹 Clone the repository
```bash
git clone https://github.com/mehedihasanmir/Sentiment-Analysis-on-IMDb-Movie-Reviews-with-pkl-file.git
cd Sentiment-Analysis-on-IMDb-Movie-Reviews-with-pkl-file
```

### 🔹 Install Dependencies
```bash
pip install -r requirements.txt
```

> If `requirements.txt` is not included, install libraries manually:
```bash
pip install pandas numpy matplotlib seaborn nltk scikit-learn
```

### 🔹 Run the Notebook
Open `moview-review.ipynb` in Jupyter Notebook or any IDE (e.g., VSCode) to explore the code.

### 🔹 Predict Using Pickle Files
```python
import pickle

# Load model and vectorizer
with open("model.pkl", "rb") as f:
    model = pickle.load(f)

with open("vectorizer.pkl", "rb") as f:
    vectorizer = pickle.load(f)

# Predict a review
text = ["This movie was absolutely fantastic!"]
text_vector = vectorizer.transform(text)
prediction = model.predict(text_vector)

print("Prediction:", prediction[0])
```

---

## 📊 Results

After evaluating all models, the one with the best performance was selected and saved. Metrics used:
- Accuracy: 88.48%
- Precision, Recall, F1-Score
- Confusion Matrix

You can visualize performance using seaborn:
```python
sns.heatmap(confusion_matrix(y_test, y_pred), annot=True, fmt='d')
```

---

## 🧠 Future Improvements

- Add deep learning models (LSTM, BERT)
- Deploy as a web application using Flask or Streamlit
- Enable real-time review input and visualization
- Add more review categories (neutral, sarcastic)

---

## 🙏 Acknowledgements

- IMDb Dataset for sentiment analysis
- NLTK and Scikit-learn developers for robust NLP and ML tools

---