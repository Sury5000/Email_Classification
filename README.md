# Email Spam Classification – Machine Learning Pipeline

This project implements a complete machine learning workflow for classifying emails as spam or ham using the SpamAssassin Public Corpus. It includes dataset downloading, email parsing, text preprocessing, feature extraction, model training, and model evaluation using precision and recall.

## Project Structure

- classification_Analysis.ipynb – Main notebook containing the full workflow  
- datasets/spamassassin/ – Downloaded dataset containing ham and spam emails  
- models/ – Optional directory for saving trained models  

## 1. Dataset Description

The dataset used is the SpamAssassin 2002 Public Corpus. It contains:

- Ham emails (legitimate messages)  
- Spam emails (phishing, advertising, unsolicited messages)

Emails are provided as raw .txt files with headers and body text.

## 2. Data Loading

A custom downloader retrieves the SpamAssassin dataset and extracts two folders:

- easy_ham  
- spam  

The notebook then:

- Removes corrupted or extremely small files  
- Parses emails using Python’s email library  
- Extracts payload (body text) using BytesParser for safe decoding  

## 3. Email Preprocessing

The preprocessing pipeline performs:

- Removal of HTML tags  
- Replacement of URLs with “URL”  
- Replacement of numbers with “NUMBER”  
- Removal of punctuation  
- Lowercasing  
- Tokenization  
- Counting word occurrences  

These steps convert raw emails into clean, standardized text suitable for machine learning models.

## 4. Feature Extraction

Two custom Scikit-Learn transformers were created:

### EmailToWordCounterTransformer  
Converts email text into a dictionary mapping each word to its count.

### WordCounterToVectorTransformer  
Transforms word-count dictionaries into bag-of-words vectors using a fixed vocabulary.

This approach produces a sparse feature matrix efficient for training classifiers.

## 5. Machine Learning Pipeline

A full Scikit-Learn pipeline was constructed combining:

- EmailToWordCounterTransformer  
- WordCounterToVectorTransformer  
- LogisticRegression classifier  

This pipeline ensures that email parsing, cleaning, vectorization, and classification are fully automated and reproducible.

## 6. Model Training

The chosen model is Logistic Regression because:

- It handles sparse, high-dimensional text data well  
- It is fast and computationally efficient  
- It produces stable and interpretable results  

The model was trained on the bag-of-words representation of the emails.

## 7. Evaluation

Model performance was assessed using:

- Precision  
- Recall  

These metrics provide insight into how well the classifier avoids false positives (misclassifying ham as spam) and false negatives (missing actual spam).

## 8. Key Insights

- Normalizing URLs, numbers, and punctuation significantly improves model accuracy.  
- Bag-of-words models remain highly effective for basic spam detection.  
- Logistic Regression provides strong performance for text classification tasks.  
- Custom transformers integrated with Scikit-Learn pipelines offer flexibility and ease of deployment.

## Conclusion

This project demonstrates a complete, production-ready text classification system:

- Email parsing  
- Text cleaning and normalization  
- Feature engineering  
- Bag-of-words vectorization  
- Model training  
- Evaluation using precision and recall  

The workflow establishes a strong foundation for more advanced spam detection systems using TF-IDF, n-grams, Naive Bayes, or deep learning approaches.
