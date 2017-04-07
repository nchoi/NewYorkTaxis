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

- Num Training Examples: 5000
- Num Testings Examples: 5000
- max: 46.949999999999996
- min: -71.3125
- std: 7.901616565823934
- var: 62.43554435330322
- mean: -0.35887041220446225
- median: -0.04000000000000048

A standard deviation of close to 8 seemed very warning. For this reason, we tried our query and python script on 100,000 entries rather than 5,000. Below is a visualization of the errors.

![Image of 100k training](https://github.com/nchoi/NewYorkTaxis/blob/master/imgs/100k_training_same_5000_test.png?raw=true)
- Num Training Examples: 100000
- Num Testings Examples: 5000
- max: 49.09
- min: -69.991959798995
- std: 6.165166883113016
- var: 38.00928269663346
- mean: -0.18568083695739432
- median: 0.24593481989708366

When we increased the training set by a factor of 20, the standard deviation decreased to about 6. That's better, but still seems like our predictive model is not very informative. At least the normal distribution is centered around a mean of about 0! 

Source code with comments will soon be available.

### Reflections
Although our predictive model wasn't very accurate, we still view this early pass at Machine Learning as a success. Perhaps a better approach would be to predict tip vs total revenue. We believe this would not only be less trivial (most of the revenue is fare, which is probably a linear function of distance between pickup neighborhood and dropoff neighborhood) but perhaps would lead to a more accurate model.

Also, another to consider if Decision Tree Regression is the best option for machine learning algorithms for this problem. We will have to experiment with other algorithms!

### Visualizations
Since our previous post, we have made big strides on data visualization! 

Here is a heat map of 200,000 points from the month of January. Unfortunately, it is not very informative in and of itself. All we can glean from here is obvious: Manhattan is the most common area for taxi pickups, with a few exceptions in the two major airports in NYC. For this reason, we prefer the visualizations below.

[Heat map](https://nchoi.github.io/NewYorkTaxis/maps/heatmap.html)  

Here is a rendering of 200k points from the month of January. It takes a surprisingly short amount of time to load these points due to several optimizations (e.g., using quadtree as underlying data structure and loading in chunks)! Here, we see more clearly the nuances of taxi pickups. 

[Quadtree based stream rendering of 200k points](https://nchoi.github.io/NewYorkTaxis/maps/canvasQuadtreeStreamRender.html)  

Here is the same visualization, but with the ability to render by a given hour. This is our favorite visualization because it tells many stories! Consider for exmaple the image below. The left plot is from 4am and the right plot is from 4pm. We hypothesize that the huge discrepancy in these two renderings can be explained by the fact that people will be commuting to Manhattan from neighboring boroughs, whereas most people will be in Manhattan at 4pm.

![Image of comparison](https://github.com/nchoi/NewYorkTaxis/blob/master/imgs/comparison.png?raw=true)

[Points with ability to render by hour](https://nchoi.github.io/NewYorkTaxis/maps/hourlyPoints.html)  

More visualizations are available on the homepage of our blog.

### The Future




