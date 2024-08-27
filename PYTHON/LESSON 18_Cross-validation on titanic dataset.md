# HOMEWORK:

## EASY: 
Add DecisionTreeClassifier to titanic data predictions. 

## HARD:
Investigate what is cross-validation and implement cross-validation on any classification model you prefer on Titanic data. Explain to each other, what do you see. 

EXAMPLE:
```py
k_fold = KFold(n_splits=10, shuffle=True, random_state=42)
accuracy_scores = cross_val_score(model_knn_cv, X, y, cv=k_fold, scoring='accuracy')
```
