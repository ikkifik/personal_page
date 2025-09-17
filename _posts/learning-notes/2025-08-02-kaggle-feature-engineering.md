---
layout: posts
title: "Kaggle: Feature Engineering"
date: 2025-08-02
category: Learning-notes
---
- Feature engineering (FE) is a "preparation step" of building machine learning model.
- It's useful for some instances: to choose which features (columns) that correspond with information we want to achieve; reveals a new "information" for problem domains; and some other common data preparation concept.

> *Consider "apparent temperature" measures like the heat index and the wind chill. These quantities attempt to measure the perceived temperature to humans based on air temperature, humidity, and wind speed, things which we can measure directly. You could think of an apparent temperature as the result of a kind of feature engineering, an attempt to make the observed data more relevant to what we actually care about: how it actually feels outside!*

- In short, applying some "things" to obtain more relevant information to reach our purpose/goal.
- With FE we can reveal features we need even though it's not preserved at the time we obtain the data, with transformation
- **Fun fact (an assumption from me):** formula equations we found on research papers, could be an approach on reaching features the author wants for model improvement. With this in mind, looking at those equations on research papers is not a pressure anymore.
- We can do train our model without feature engineering first (maybe slightly), but do feature engineering later, to compare the performance between those 2 conditions. Here we make a baseline score, also to assess whether our new dataset brings improvement or not.
- **Feature ratio** = amount of new features compared to the initial amount of features.


- **Feature utility metric**, a function measuring associations between a feature and the target.
	- Mutual information: able to detect any kind of relationship
	- Correlation: only detect linear relationship
- Uncertainty can be meaning as scattered points in visual. For examples, when we try to visualize category of housing prices based on its exterior quality, we obtain 4 classes: Fair, Typical, Good, and Excellent. The method we choose are able to make a useful visualization since it forms a good separation for each data category, this can lead to a conclusion that "exterior quality" has good impact on reducing uncertainty of features.

>***Technical note**: What we're calling uncertainty is measured using a quantity from information theory known as "**entropy**". The **entropy** of a variable means roughly: "how many yes-or-no questions you would need to describe an occurance of that variable, on average." The more questions you have to ask, the more uncertain you must be about the variable. Mutual information is how many questions you expect the feature to answer about the target.*

- Mutual information (MI) is a univariate metrics, it means it cannot detects interactions between features (more than one feature).
- MI used to understand the relative potential of a feature.
- Even though after we use MI to find a high feature score that possibly contributed to our model, it doesn't rule out the possibility that other features also could have an important contribution yet having low MI score, here's the important **domain knowledge** play a role.


### Creating Features

> **Tips on Discovering New Features**
> - Understand the features. Refer to your dataset's _data documentation_, if available.
> - **Research the problem domain** **to acquire** **domain knowledge**. If your problem is predicting house prices, do some research on real-estate for instance. Wikipedia can be a good starting point, but books and [journal articles](https://scholar.google.com/) will often have the best information.
> - **Study previous work**. [Solution write-ups](https://www.kaggle.com/sudalairajkumar/winning-solutions-of-kaggle-competitions) from past Kaggle competitions are a great resource.
> - **Use data visualization.** Visualization can reveal pathologies in the distribution of a feature or complicated relationships that could be simplified. Be sure to visualize your dataset as you work through the feature engineering process.


- **The "Counts" chapter** discussed about how we can describe features for feature engineering, for instance how many feature we can do formulation, or how many features are not empty (Nan, null, False, etc), there is nothing to do further on this chapter actually.
- Group Transforms (basically grouping or groupby for aggregation), if there is a category (features) interaction.

> **Tips on Creating Features**  
> It's good to keep in mind your model's own strengths and weaknesses when creating features. Here are some guidelines:
> - Linear models learn sums and differences naturally, but can't learn anything more complex.
> - Ratios seem to be difficult for most models to learn. Ratio combinations often lead to some easy performance gains.
> - Linear models and neural nets generally do better with normalized features. Neural nets especially need features scaled to values not too far from 0. Tree-based models (like random forests and XGBoost) can sometimes benefit from normalization, but usually much less so.
> - Tree models can learn to approximate almost any combination of features, but when a combination is especially important they can still benefit from having it explicitly created, especially when data is limited.
> - Counts are especially helpful for tree models, since these models don't have a natural way of aggregating information across many features at once.


### Clustering with K-means
- Unsupervised learning don't look at the data target; instead it purposely learn some property of the data.
- Unsupervised algorithm can be used as "feature discovery" in feature engineering for prediction.
- Cluster labels as a (new) feature. `Clustering acts like a traditional "binning" or "discretization" transform. On multiple features, it's like "multi-dimensional binning" (sometimes called vector quantization).`
- Cluster feature (label) is categorical, shown with a label encoding.
- Can be used for break up complicated data relationship into simple **chunk**, then use the chunk to train the model one-by-one instead the whole at once.
- Clustering algorithm differs by how they measure "similarity" or "proximity" and what kind of features they work with.
- "K" in "K-means" is how many **centroid** or cluster group it creates, we defined it by ourselves.
- **Voronoi tessallation** forms line after points of different centroid overlap each other.
- Feature space
- `max_iter`=iteration of building each cluster, `n_clusters`=how many clusters/centroid, `n_init`=number of iteration where centroid moving?
- there is no best or one-for-all solution, it's all depends on the model algorithm we're using and what we're trying to predict. The best approach is through hyperparameter tuning (cross-validation).


 - Making decision of whether data needs to rescale or not, depends on some domain knowledge of the data, usually it comes spontaneously, instinctively.

- we can use PCA as a descriptive to see variation of our features, whether a feature is more important than the other; or
- we can also use PCA as a features, for example dimensionality reduction, **anomaly detection**, and many more.


- Target Encoding, similarly with one-shot encoding and label encoding (ordinal), the different is it also includes the target feature to create encoding. This make it called supervised feature engineering technique.
- Using target encoding face some drawbacks, to get over it we can use **smoothing**. It is an approach where we blend **in-category average** with **overall category average**, then apply weight on the calculation
```
encoding = weight * in_category + (1 - weight) * overall
```

- To know how to get weight we use below formula, where `n` is the occurrence of the category appears in data, and `m` is our smoothing factor that we define by ourself. *Larger values of `m` put more weight on the overall estimate.* *When choosing a value for `m`, consider how noisy you expect the categories to be.*
```
weight = n / (n + m)
```

- For example, where:
	- Number of occurrence of Chevrolet: 3
	- m = 2.0 
	- weight = 3 / (3 + 2.0) = 3 / 5 = 0.6
- Then the formula would be
```
chevrolet = 0.6 * 6000.00 + 0.4 * 13285.03
```
	
---
**Notes:**
- Split means, fractioning rows

---
**Questions:**
1. What is "relationship"? Which one is it? What kind of it?
	- A connection of features that can reveal a new information, feature connect with other feature to make a more sound information(?)

