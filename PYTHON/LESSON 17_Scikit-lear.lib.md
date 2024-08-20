# TEAMWORK



# Scikit-learn library

https://scikit-learn.org/stable/

https://scikit-learn.org/stable/modules/generated/sklearn.linear_model.LinearRegression.html

___
## 1. What is an error rate?
   
An error rate in machine learning is a metric that quantifies the proportion of incorrect predictions made by a model.
In scikit-learn, if you know the accuracy (how often the model is correct), you can easily find the error rate:

<img width="265" alt="Screenshot 2024-08-20 at 18 42 06" src="https://github.com/user-attachments/assets/d5d1273f-fc2d-4c37-96fb-81d2a7cf5883">

Example: Assuming y_true are the actual labels and y_pred are the predicted labels
```py
from sklearn.metrics import accuracy_score
accuracy = accuracy_score(y_true, y_pred)
error_rate = 1 - accuracy
```

The error rate tells you how reliable your model is. A lower error rate means your model is more accurate and trustworthy.
   
___
## 2. Where you could use other machine-learning models?
Machine learning models help solve real-world problems by making predictions, optimizing processes, and uncovering patterns across diverse fields, from healthcare to finance, retail, and beyond. Each industry leverages specific models and techniques tailored to its unique challenges and data types.

**Key Areas Where Machine Learning is Used:**
- **Healthcare:** Disease diagnosis, medical imaging, and personalized treatment.
- **Finance:** Credit scoring, fraud detection, and algorithmic trading.
- **Marketing:** Customer segmentation, sales prediction, and recommendation systems.
- **Transportation:** Autonomous vehicles, traffic prediction, and predictive maintenance.
- **NLP (Natural Language Processing):** Sentiment analysis, machine translation, and chatbots.
- **Retail:** Inventory management, dynamic pricing, and customer lifetime value prediction.
- **Manufacturing:** Quality control, predictive maintenance, and supply chain optimization.
- **Agriculture:** Crop yield prediction, pest detection, and precision farming.
- **Energy:** Consumption forecasting, fault detection, and smart grid management.
- **Entertainment:** Content recommendation, automated content creation, and personalized advertising.
- **Security:** Intrusion detection, facial recognition, and spam filtering.
- **Environmental Science:** Climate modeling, wildlife conservation, and natural disaster prediction.
- **Human Resources:** Employee attrition prediction, resume screening, and workforce planning.
  
___
## 3. What is the difference between supervised and unsupervised training?
The difference between supervised and unsupervised training in machine learning lies in how the models learn from the data and the type of tasks they are used for.
**Key Differences:**

a) Labels:

- Supervised Learning: Uses **labeled data** (input-output pairs).
- Unsupervised Learning: Uses **unlabeled data** (only inputs).
  
b) Objective:

- Supervised Learning: Predict an outcome or label for new data based on the learning from labeled examples.
- Unsupervised Learning: Discover hidden patterns, structures, or relationships in the data.
  
c) Typical Applications:

- Supervised Learning: Used for tasks like classification (e.g., identifying emails as spam or not) and regression (e.g., predicting house prices).
- Unsupervised Learning: Used for tasks like clustering (e.g., customer segmentation) and dimensionality reduction (e.g., simplifying large datasets).

In essence, supervised learning is about learning from examples with known outcomes, while unsupervised learning is about exploring data to find hidden structures without explicit guidance.
___
## 4. How to import different models from the scikit-learn package?
You use `import` statement in Python.

Scikit-learn provides a wide range of models for classification, regression, clustering, and other tasks.

Some examples: 
```py
from sklearn.datasets import load_iris
from sklearn.model_selection import train_test_split
from sklearn.neighbors import KNeighborsClassifier
from sklearn.metrics import accuracy_score
```
___
## 5. How can you evaluate the performance of a machine learning model in scikit-learn?

1. Split the data into training and testing sets.
2. Train the model on the training data.
3. Make Predictions on the test data.
4. Evaluate performance using metrics like accuracy, precision, recall, F1-score, and others.
5. Perform Cross-Validation to ensure the model generalizes well.
6. Tune Hyperparameters to improve performance.
7. Analyze Learning Curves to understand model behavior with different training sizes.

Code example:
```py
# Import necessary modules from scikit-learn
from sklearn.datasets import load_iris
from sklearn.model_selection import train_test_split, cross_val_score, GridSearchCV, learning_curve
from sklearn.neighbors import KNeighborsClassifier
from sklearn.metrics import accuracy_score, precision_score, recall_score, f1_score, confusion_matrix, roc_curve, roc_auc_score
import matplotlib.pyplot as plt

# 1. Load Data
iris = load_iris()
X = iris.data
y = iris.target

# 2. Split the Data
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.3, random_state=42)

# 3. Initialize the Model
model = KNeighborsClassifier()

# 4. Train the Model
model.fit(X_train, y_train)

# 5. Make Predictions
y_pred = model.predict(X_test)
y_prob = model.predict_proba(X_test)[:, 1]  # Probabilities for ROC AUC

# 6. Evaluate Performance
# Calculate Accuracy
accuracy = accuracy_score(y_test, y_pred)
print(f"Accuracy: {accuracy * 100:.2f}%")

# Compute Precision, Recall, and F1 Score
precision = precision_score(y_test, y_pred, average='weighted')
recall = recall_score(y_test, y_pred, average='weighted')
f1 = f1_score(y_test, y_pred, average='weighted')
print(f"Precision: {precision:.2f}")
print(f"Recall: {recall:.2f}")
print(f"F1 Score: {f1:.2f}")

# Confusion Matrix
conf_matrix = confusion_matrix(y_test, y_pred)
print("Confusion Matrix:")
print(conf_matrix)

# ROC Curve and AUC (Only for binary classification - so it's an example here)
# For multi-class problems, ROC AUC needs to be computed for each class.
fpr, tpr, _ = roc_curve(y_test, y_prob, pos_label=1)  # Example for binary class; pos_label needs to be adjusted
auc = roc_auc_score(y_test, y_prob)
plt.plot(fpr, tpr, marker='.')
plt.xlabel('False Positive Rate')
plt.ylabel('True Positive Rate')
plt.title(f'ROC Curve (AUC = {auc:.2f})')
plt.show()

# 7. Cross-Validation
scores = cross_val_score(model, X, y, cv=5)
print(f"Cross-Validation Scores: {scores}")
print(f"Mean CV Score: {scores.mean():.2f}")

# Hyperparameter Tuning (Grid Search)
param_grid = {'n_neighbors': [1, 3, 5, 7, 9]}
grid_search = GridSearchCV(KNeighborsClassifier(), param_grid, cv=5)
grid_search.fit(X_train, y_train)
print(f"Best Parameters: {grid_search.best_params_}")
print(f"Best Score: {grid_search.best_score_:.2f}")

# 8. Learning Curves
train_sizes, train_scores, test_scores = learning_curve(model, X, y, cv=5)
plt.plot(train_sizes, train_scores.mean(axis=1), label='Training score')
plt.plot(train_sizes, test_scores.mean(axis=1), label='Cross-validation score')
plt.xlabel('Number of Training Samples')
plt.ylabel('Score')
plt.title('Learning Curves')
plt.legend()
plt.show()
```

___
## 6. What metrics are commonly used for evaluation?
To evaluate a machine learning model effectively, you should choose appropriate metrics based on the type of problem you're working on:
- **Classification:** Accuracy, Precision, Recall, F1-Score, Confusion Matrix, ROC Curve, AUC.
- **Regression:** MAE, MSE, RMSE, R-Squared.
- **Clustering:** Silhouette Score, Davies-Bouldin Index, Calinski-Harabasz Index.
  
Using these metrics helps you understand your model’s strengths and weaknesses, and guides you in improving its performance.

___
## 7. What is model overfitting, and how can it be prevented?

- Model overfitting occurs when a machine learning model learns the training data too well, capturing noise and details that do not generalize to unseen data. As a result, the model performs exceptionally well on the training set but poorly on new, unseen data. Overfitting typically leads to high variance and poor generalization.
  
- Preventing overfitting involves balancing model complexity and ensuring that the model generalizes well to unseen data. Key strategies include simplifying the model, applying regularization, using cross-validation, pruning, stopping training early, increasing the training data, selecting relevant features, and using ensemble methods. By implementing these techniques, you can improve the model’s ability to generalize and avoid overfitting.
___
