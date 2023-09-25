---
layout: post
title: Direct Marketing
description: Predictive analytics with random forest, decision trees, KNN, linear regression, and logistic regression.
image:
---



## Predictive Analytics

### Summary
Can the type of spender be predicted based on household data for direct mailers?

This project was a collaborative effort between two other teammates. The project’s goal was to predict what type of spender a potential customer would be based on household characteristics. The spending types were low, medium, and high. By predicting a type of spender someone would be, one can directly market those that would spend more than those that would spend less. We implemented five different types of models and compared them to see which yield the highest accuracy score.

### Modeling Methods
* K-Nearest Neighbors
* Decision Tree
* Linear Regression
* Logistic Regression
* Random Forest

### Results
Our results led to the random forest having the highest accuracy score overall of predicting the correct type of spender 82% of the time. However, we concluded that further data would need to be gathered if a company were to implement this model with the variables given.

### Project Preview
#### Random Forest Model
```
rfc_3 = RandomForestClassifier(n_estimators = 1577,
                               min_samples_split = 10,
                               min_samples_leaf = 1,
                               max_features = 'sqrt',
                               max_depth = 20,
                               bootstrap = True)

# fit the training set
rfc_3.fit(X_train, y_train)

# make predictions
y_pred = rfc_3.predict(X_valid)
accuracy_score(y_valid, y_pred)

# confusion matrix
conf_matrix_rf = pd.DataFrame(confusion_matrix(y_valid, y_pred, labels=['High','Med','Low']),
  index = ['actual high', 'actual med', 'actual low'],
  columns = ['predicted high', 'predicted med', 'predicted low'])

# plot the matrix
fig, ax = plt.subplots(figsize = (10,8))

sns.heatmap(conf_matrix_rf/np.sum(conf_matrix_rf), annot=True,
            fmt='.2%', cmap='Blues', annot_kws={'size':15})

ax.set_title('Random Forest Confusion Matrix', fontsize = 18, loc='left')

ax.set_xticklabels(ax.get_xmajorticklabels(), fontsize = 12)
ax.set_yticklabels(ax.get_ymajorticklabels(), fontsize = 12)

plt.show()
```
The confusion matrix shows the precision score, with 83.67% were predicted as high spenders when they were actually high spenders. 70% were predicted as medium spenders when they were actually medium, and 85.59% were predicted as low spenders when they were actually low.

![Random Forest Confusion Matrix](/assets/images/directmarketingrf.JPG)


### The Complete Project
<section id="Repository">
	<div class="inner">
    <ul class="actions fit small">
      <li><a href="https://github.com/Torreylee1028/Direct-Marketing" target="_blank" class="button small">View Repository</a></li>
    </ul>
	</div>
</section>
