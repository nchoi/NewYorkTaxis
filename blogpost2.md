# Blog #2

### This Week's Work
This week, we worked on learning how to use scikit-learn and started doing some machine learning explorations on our database. Also, we improved some visualizations since the midterm report! These two parts are explained below.

### Machine Learning
Here we are going to present one of our recent attempts at using machine learning on our data.

Our goal was to predict from a ride's pick-up neighborhood, drop-off neighborhood, and time of day what the total revenue (including tip) would be for that ride.

To do this, first we had to run a SQL query to select the following features of each ride:
- pickup_id
- dropoff_id
- timestamp
- total_revenue

The first three features would be the features of our X feature vector. The y feature, which we wanted to predict, was the timestamp.

After running this SQL query (once for the training set and once for the test set) for 5000 entries, we ran into a predicament! We wanted to use a regression algorithm to predict the total, but two out of three of our features (pickup_id and dropoff_id) were categorical features rather than continuous values. Luckily, [scikit-learn had a useful way to do some preprocessing](http://scikit-learn.org/stable/modules/preprocessing.html#encoding-categorical-features) each feature into a continuous variable.

```
def do_encoding(feature_vectors):
    enc = preprocessing.OneHotEncoder()
    enc.fit_transform(feature_vectors)
    return feature_vectors
```

After preprocessing our feature vectors, we were ready to apply [Decision Tree Regression](http://scikit-learn.org/stable/auto_examples/tree/plot_tree_regression.html#sphx-glr-auto-examples-tree-plot-tree-regression-py). Using the sci-kit code below, we were able to predict the revenue of each ride in the test feature vectors. 
```
    clf = tree.DecisionTreeRegressor()
    clf = clf.fit(list_of_train_feature_vectors, train_y)
    clf.predict(list_of_test_feature_vectors)
```
Using these predictions, we calculated the errors and visualized them. Below is the error for 5000 entries.
![Image of 5k training](https://github.com/nchoi/NewYorkTaxis/blob/master/imgs/5000_training_5000_test.png?raw=true)

*Wow, a normal distribution!*

Using scipy, we were then able to get these interesting values **for the errors**.
| Property      | Value         |
| ------------- |:-------------:|
| # of training | 5000          |
| # of test     | 5000          |
| max           | 46.95         |

![Image of 100k training](https://github.com/nchoi/NewYorkTaxis/blob/master/imgs/100k_training_same_5000_test.png?raw=true)

Labeled data - have to deal with our own labels, track taxis over time
Categorical


Source code will soon be available.

### Visualizations

### The Future



