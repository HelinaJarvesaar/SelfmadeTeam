# HOMEWORK:

## EASY: 

Add DecisionTreeClassifier to titanic data predictions. 
```py
from sklearn.tree import DecisionTreeClassifier

model = DecisionTreeClassifier(random_state=42)
model.fit(X_train, y_train)

prediction_result = model.predict(X_test)
prediction_result
```
<img width="541" alt="Screenshot 2024-08-30 at 21 13 00" src="https://github.com/user-attachments/assets/257418c5-2097-4bf6-bf0f-7090af72f9c0">




## HARD:

Investigate what is cross-validation and implement cross-validation on any classification model you prefer on Titanic data. Explain to each other, what do you see. 

EXAMPLE:
```py
k_fold = KFold(n_splits=10, shuffle=True, random_state=42)
accuracy_scores = cross_val_score(model_knn_cv, X, y, cv=k_fold, scoring='accuracy')
```

### Cross-validation

Cross-validation is a statistical technique used in machine learning to assess how well a model generalizes to an independent dataset (i.e., how well it performs on data it has never seen before). It is especially useful when you want to evaluate the performance of a model while avoiding overfitting and ensuring that the evaluation is not biased by a particular train-test split.
Example:
```py
from sklearn.datasets import load_iris
from sklearn.model_selection import cross_val_score, KFold
from sklearn.tree import DecisionTreeClassifier
import numpy as np

# Load the Iris dataset
iris = load_iris()
X = iris.data
y = iris.target

# Initialize a Decision Tree Classifier
model = DecisionTreeClassifier()

# Set up K-Fold Cross-Validation with 5 folds
kf = KFold(n_splits=5, shuffle=True, random_state=42)

# Perform cross-validation
scores = cross_val_score(model, X, y, cv=kf) # cv = cross-validation

# Print the cross-validation scores in a formatted way
formatted_scores = ", ".join(f"{score:.2f}" for score in scores)
mean_accuracy = scores.mean()

# Print the cross-validation scores
print(f"Cross-validation scores: {formatted_scores}")
print(f"Mean accuracy: {mean_accuracy:.2f}")
```
<img width="516" alt="Screenshot 2024-08-30 at 21 41 48" src="https://github.com/user-attachments/assets/f5f7b6bb-03d7-473b-a0cc-6e10b4653222">



### What the Code Does:

- Load the Dataset: 

  The Iris dataset is loaded, which is a simple dataset with 150 samples of iris flowers, classified into three different species.

- Initialize the Model:

  A Decision Tree Classifier is used as the model.

- K-Fold Cross-Validation: 

  The KFold class is used to split the data into 5 folds. The shuffle=True parameter shuffles the data before splitting to ensure randomness.

- Cross-Validation: 

  cross_val_score is used to perform cross-validation. It trains the model on K-1 folds and tests it on the remaining fold. This is repeated for all folds.

- RESULT:
  The cross-validation scores for each fold are printed, along with the mean accuracy across all folds.

