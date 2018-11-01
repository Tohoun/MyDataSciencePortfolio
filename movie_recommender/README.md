<h1 align="center"> Movie Recommender Systems </h1> <br>
<p align="center">
  <a href="https://s3.amazonaws.com/re-work-production/post_images/524/netflixf/original.png?1519061395">
    <img alt="Recommender Systems" title="Recommender Systems" src="https://s3.amazonaws.com/re-work-production/post_images/524/netflixf/original.png?1519061395">
  </a>
</p>

<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->

## Contents
![Python](https://img.shields.io/badge/python-v3.6+-blue.svg)
![Dependencies](https://img.shields.io/badge/dependencies-up%20to%20date-brightgreen.svg)

- [Recommender System Overview](#recommender-system-verview)
   - [Collaborative Filtering](#collaborative-filtering)
   - [Content-based Filtering](#content-based-filtering)
   - [Hybrid Recommender](#hybrid-recommender)
   - [Common Challenges](#common-challenges)
   - [Solution](#solution)

- [Movie Recommender System Development](#movie-recommender-system-development)

  - [Movie Recommendation Engine Development with KNN](https://github.com/KevinLiao159/MyDataSciencePortfolio/blob/master/movie_recommender/movie_recommendation_using_KNN.ipynb)
  - [Movie Recommendation Engine Development with ALS in Apache Spark](https://github.com/KevinLiao159/MyDataSciencePortfolio/blob/master/movie_recommender/movie_recommendation_using_ALS.ipynb)
  - [Movie Recommendation Engine Development with Neural Networks in Keras](https://github.com/KevinLiao159/MyDataSciencePortfolio/blob/master/movie_recommender/movie_recommendation_using_NeuMF.ipynb)

- [Source Code](https://github.com/KevinLiao159/MyDataSciencePortfolio/tree/master/movie_recommender/src)
  - [Movie Recommender with KNN Item Based Collaborative Filtering](https://github.com/KevinLiao159/MyDataSciencePortfolio/blob/master/movie_recommender/src/knn_recommender.py)
  - [Movie Recommender with Alternative Least Square Matrix Factorization](https://github.com/KevinLiao159/MyDataSciencePortfolio/blob/master/movie_recommender/src/als_recommender.py)
  - [Movie Recommender with Neural Collaborative Filtering](https://github.com/KevinLiao159/MyDataSciencePortfolio/blob/master/movie_recommender/src/neural_recommender.py)

- [References](#references)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

## Recommender System Overview
A recommender system is a subclass of information filtering system that seeks to predict the "rating" or "preference" a user would give to an item. Recommender systems are utilized in a variety of areas including movies, music, news, social tags, and products in general. Recommender systems typically produce a list of recommendations in one of two ways – through collaborative filtering or through content-based filtering.

#### Collaborative Filtering
This approach builds a model from a user's past behaviour (items previously purchased or selected and/or numerical ratings given to those items) as well as similar decisions made by other users. This model is then used to predict items (or ratings for items) that the user may have an interest in

#### Content-based Filtering
This approach utilizes a series of discrete characteristics of an item in order to recommend additional items with similar properties

#### Hybrid Recommender
This one combines the previous two approaches

#### Common Challenges
In my project, I will focus on building a collaborative filtering engine. In collaborative filtering, there are typically following challenges:
* cold start
* data sparsity
* popular bias (how to recommend products from the tail of product distribution)
* scalability (computation grows as number of users and items grow)
* pool relationship between like-minded yet sparse users

<p align="center">
  <a href="https://github.com/KevinLiao159/MyDataSciencePortfolio/blob/master/movie_recommender/movie_recommendation_using_KNN.ipynb">
    <img alt="Long Tail Property in Ratings Distribution" title="Long Tail Property in Ratings Distribution" src="https://media.springernature.com/lw785/springer-static/image/chp%3A10.1007%2F978-3-319-29659-3_2/MediaObjects/334607_1_En_2_Fig1_HTML.gif">
  </a>
</p>

Above chart is the distribution of item rating frequency. This distribution often satisfies a property in real-world settings, which is referred to as [the long-tail property [1]](https://www.springer.com/cda/content/document/cda_downloaddocument/9783319296579-c1.pdf?SGWID=0-0-45-1554478-p179516130). According to this property, only a small fraction of the items are rated frequently. Such items are referred to as popular items. The vast majority of items are rated rarely. 

In most cases, high-frequency items tend to be relatively competitive items with little profit for the merchant. On the other hand, the lower frequency items have larger profit margins. However, many recommendation algorithms have a tendency to suggest popular items rather than infrequent items. This phenomenon also has a negative impact on diversity, and users may often become bored by receiving the same set of recommendations of popular items

#### Solution
Use matrix factorization technique to train model to learn user-item interaction by capturing user information in user latent factors and item information in item latent factors. Meanwhile, matrix factorization technique can significantly reduce dimensionality and sparsity and it will reduce huge amount of memory footprint and make our system more scalable


## Movie Recommender System Development
In this project, I focus on collaborative filtering recommender systems since they are widely used and well research in many different business and consistently provide good business values. It'd be very cool I can develop **Movie Recommender Systems** for myself. Let's see what movie recommendations my recommender offers me.

#### Datasets
I use [MovieLens Datasets [2]](https://grouplens.org/datasets/movielens/latest/). This dataset describes 5-star rating and free-text tagging activity from MovieLens, a movie recommendation service. It contains 27753444 ratings and 1108997 tag applications across 58098 movies. These data were created by 283228 users between January 09, 1995 and September 26, 2018. This dataset was generated on September 26, 2018.

#### Models
I start with basic and easy-implment models for my recommender system. As I want to improve my system's recommendations, I use more complex models. Eventually, I use neural networks for the recommender system. Following is the list of three models I'd like to use.
 - **KNN Item Based Collaborative Filtering**
 - **Alternating Least Square** (ALS) Matrix Factorization
 - **Neural Collaborative Filtering** Approach


### [Movie Recommendation Engine Development with KNN](https://github.com/KevinLiao159/MyDataSciencePortfolio/blob/master/movie_recommender/movie_recommendation_using_KNN.ipynb)
Collaborative filtering based systems use the actions of users to recommend other items. In general, they can either be user-based or item-based. Item-based approach is usually prefered than user-based approach. User-based approach is often harder to scale because of the dynamic nature of users, whereas items usually don't change much, so item-based approach often can be computed offline.

KNN is a perfect go-to model for this use case and KNN is a very good baseline for recommender system development. In item-based collaborative filtering, KNN will use a pre-defined distance metric to find clusters of similar items based on users' ratings, and make recommendations using the distance metric in item ratings of top-k [nearest neighbors [1]]((https://www.springer.com/cda/content/document/cda_downloaddocument/9783319296579-c1.pdf?SGWID=0-0-45-1554478-p179516130)).

#### Let's Make Some Recommendations
"Iron Man" is one of my favorite movies so I want to test what movie recommendations my system is giving me. It's very cool to see my recommender system give me recommendations

Check out detailed source code and instruction of commands (see the parse_args function) in [knn_recommender.py](https://github.com/KevinLiao159/MyDataSciencePortfolio/blob/master/movie_recommender/src/knn_recommender.py)

Run KNN recommender system:
```
python src/knn_recommender.py --movie_name "Iron Man" --top_n 10
```

Output:
```
You have input movie: Iron Man
Found possible matches in our database: ['Iron Man (2008)', 'Iron Man 3 (2013)', 'Iron Man 2 (2010)']

Recommendation system start to make inference ...
It took my system 1.38s to make inference
Recommendations for Iron Man:
1: Bourne Ultimatum, The (2007), with distance of 0.4221
2: Sherlock Holmes (2009), with distance of 0.4194
3: Inception (2010), with distance of 0.3934
4: Avatar (2009), with distance of 0.3836
5: WALL·E (2008), with distance of 0.3835
6: Star Trek (2009), with distance of 0.3753
7: Batman Begins (2005), with distance of 0.3703
8: Iron Man 2 (2010), with distance of 0.3703
9: Avengers, The (2012), with distance of 0.3581
10: Dark Knight, The (2008), with distance of 0.3013
```

It's interesting that the recommended movies are from the same time period as "Iron Man". These movies were as much popular as "Iron Man" at that time. This is exactly the downside of item-based collaborative filtering system. It always offers users the same set of very popular items. Users might get bored at same point without seeing diversity of recommendations


### [Movie Recommendation Engine Development with ALS in Apache Spark](https://github.com/KevinLiao159/MyDataSciencePortfolio/blob/master/movie_recommender/movie_recommendation_using_ALS.ipynb)
**Alternating Least Square (ALS)** is one of state-of-the-art **Matrix Factorization** models under the context of distributed computing.

Matrix Factorization is simply a mathematical operation for matrices. It is usually more effective in collaborative filtering, because it allows us to discover the latent (hidden) features underlying the interactions between users and items (movies).

Advantages of collaborative filtering using Matrix Factorization:
* No need to know about item content
* "Item cold-start" problem is avoided
* User interest may change over time
* Explainability

There are matrix factorization methods such as **Singular Value Decomposition (SVD)** and **Non-Negative Matrix Factorization (NMF)**. I chose [Alternating Least Square (ALS) implemented in Spark](https://spark.apache.org/docs/preview/ml-collaborative-filtering.html#collaborative-filtering) because it is a parallel algorithm designed for a large-scale collaborative filtering problems (such as the Netflix Prize). This method is doing a pretty good job at resolving scalability and sparseness of the user profiles, and it's simple and scales well to very large datasets.

The basic ideas behind ALS are:
* Factorize a big matrix into two small matrix (A = Users * Items)
* Use two loss functions for gradient descent
* Alternative gradient descent between Users and Items matrices back and forth

If you are interested in the math part behind ALS, please read [Large-scale Parallel Collaborative Filtering for the Netflix Prize [3]](https://endymecy.gitbooks.io/spark-ml-source-analysis/content/%E6%8E%A8%E8%8D%90/papers/Large-scale%20Parallel%20Collaborative%20Filtering%20the%20Netflix%20Prize.pdf)

Hyperparameter tuning in Alternating Least Square:
* maxIter: the maximum number of iterations to run (defaults to 10)
* rank: the number of latent factors in the model (defaults to 10)
* regParam: the regularization parameter in ALS (defaults to 1.0)

#### Let's Make Some Recommendations







I choose to use two types of different ML algos to build two separate movie recommendation engines and compare their performance and results respectively. The following is the list of my ML algos to implement movie recommendation engine
* [Alternating Least Square (ALS) Matrix Factorization](https://spark.apache.org/docs/preview/ml-collaborative-filtering.html#collaborative-filtering)
* [Neural Collaborative Filtering Approach](https://arxiv.org/pdf/1708.05031.pdf)
  * Generalized Matrix Factorization (GMF)
  * Multi-Layer Perceptron (MLP)
  * Neural Matrix Factorization (NeuMF)

> Model Performance Comparison on Test Datasets

| MODEL | MEAN SQUARED ERROR | ROOT MEAN SQUARED ERROR |
| --- | --- | --- |
| ALS | 0.8475 | 0.9206 |
| - | - | - |
| GMF | 0.8532 | 0.9237 |
| MLP | 0.8270 | 0.9094 |
| NeuMF | 0.8206 | 0.9059 |


### Movie Recommendation Engine Development in Apache Spark
In the context of distributed computing and large scale machine learning, Alternating Least Square (ALS) in Spark ML is definitely the one of the first go-to models for collaborative filtering in recommender system. ALS algo has been proven to be very effective for both explicit and implicit feedback datasets. 

In addition, [Alternating Least Squares with Weighted λ Regularization (ALS-WR)](https://endymecy.gitbooks.io/spark-ml-source-analysis/content/%E6%8E%A8%E8%8D%90/papers/Large-scale%20Parallel%20Collaborative%20Filtering%20the%20Netflix%20Prize.pdf) is a parallel algorithm designed for a large-scale collaborative filtering challenge, the Netflix Prize. This method is meant to resolve scalability and sparseness of the user profiles, and it's simple and scales well to very large datasets

* Advantages of collaborative filtering over content based methods
  * No need to know about item content
  * "Item cold-start" problem is avoided
  * User interest may change over time
  * Explainability

* My implementation to train the best ALS model via cross-validation and hyperparam-tuning

```python
from src.spark_recommender_system import Dataset, train_ALS
from pyspark.ml.evaluation import RegressionEvaluator

# config
SEED = 99
MAX_ITER = 10
SPLIT_RATIO = [6, 2, 2]
DATAPATH = './data/movie/ratings.csv'

# construct movie ratings dataset object
rating_data = Dataset(spark, DATAPATH)
# get rating data as Spark RDD
rating_rdd = rating_data.RDD
# get train, validation, and test data
train_data, validation_data, test_data = rating_data.split_data(rating_rdd, SPLIT_RATIO, SEED)
# create a hyperparam tuning grid
regParams = [0.05, 0.1, 0.2, 0.4, 0.8]
ranks = [6, 8, 10, 12, 14]
# train models and select the best model in hyperparam tuning
best_model = train_ALS(train_data, validation_data, MAX_ITER, regParams, ranks)
# test model
predictions = best_model.transform(test_data)
evaluator = RegressionEvaluator(metricName="rmse", labelCol="rating",
                                predictionCol="prediction")
rmse = evaluator.evaluate(predictions)
print("Root-mean-square error = " + str(rmse))
```

### Movie Recommendation Engine Development in Neural Networks with Keras
[Neural Collaborative Filtering (NCF)]((https://arxiv.org/pdf/1708.05031.pdf)) is a paper published by National University of Singapore, Columbia University, Shandong University, and Texas A&M University in 2017. It utilizes the flexibility, complexity, and non-linearity of Neural Network to build a recommender system. It proves that Matrix Factorization, a traditional recommender system, is a special case of Neural Collaborative Filtering. In addition, it shows that NCF outperforms the state-of-the-art models in two public datasets

Before we get into the Keras implementation of Neural Collaborative Filtering (NCF), let's quickly review Matrix Factorization and how it is implemented in the context of Neural Networks.

Here is the illustration of the math:
![Matrix factorization](https://cdn-images-1.medium.com/max/2000/1*WrOoSr49lQs43auSsLlLdg.png)

Essentially, each user and item is projected onto a latent space, represented by a latent vector. The more similar the two latent vectors are, the more related the corresponding users’ preference. Since we factorize the user-item matrix into the same latent space, we can measure the similarity of any two latent vectors with cosine-similarity or dot product.

In Neural Network, we will implement an embedding layer. We usually map a user one-hot encoded vector to a user embedded vector, and map a item one-hot encoded vector to an item vector. Then we will do a element-wise multiplication between user latent vector and item latent vector. Now we have a element-wise user-item latent vector. 

In traditional matrix factorization, we would just sum up the vector, which is also the dot product of user latent vector and item latent vector. Then we minimize the loss between the dot product of these two and the true ratings in user-item association matrix

However, in the world of neural network, we can generalize matrix factorization by feeding the element-wise user-item latent vector into FC layer. The Neural FC layer can be any kind neuron connections. With the complicated connection and non-linearity in the Neural CF layers, this model is capable of properly estimating the complex interactions between user and item in the latent space. Then the objective function is to minimize the loss between the predictions and the ratings. This is exactly how Generalized Matrix Factorization (GMF) is implemented. Below is the graph of network architecture:
![Generalized Matrix Factorization (GMF)](https://cdn-images-1.medium.com/max/2000/1*EA03sZsfJ4wu8yMoU6xwPQ.png)

To further generalize the process of matrix factorization in neural network, we need to increase the complexity in hypothesis space of the network and remove calucation rules from the neural topology. This means we will remove the element-wise multiplication layer and add more Neural CF layers, for example, multiple layer perceptron (MLP), can be placed after the concat layer of user and item embedded layers. And this is the Multi-Layer Perceptron (MLP) model. Below is the graph of network architecture:
![Multi-Layer Perceptron (MLP)](https://cdn-images-1.medium.com/max/1600/1*sTBtqrsQzTKlZ8hSU7I6FQ.png)

Now that we understand how generalized matrix factorization works in the world of neural network, the next question is how we can improve the model. One simple trick that is often used in Machine Learning competitions is "stacking". In neural networks, "stacking" means we concat the outputs of GMF and MLP networks and connect it with the sigmoid activation output layer. And this is Neural Matrix Factorization (NeuMF). Below is the graph of network architecture:
![Neural Matrix Factorization (NeuMF)](https://cdn-images-1.medium.com/max/1600/1*CoETyuU36fshduKAfFhCrg.png)

* My implementation to build Neural Matrix Factorization (NeuMF) and train the model


```python
import pandas as pd
from src.neural_recommender_system import (get_GMF_model,
                                           get_MLP_model,
                                           get_NeuMF_model,
                                           train_model,
                                           load_trained_model)
# data config
DATAPATH = './data/movie/ratings.csv'
# MODELPATH = './data/movie/tmp/model.hdf5'
SEED = 99
TEST_SIZE = 0.2

# model config
EMBEDDED_DIM = 10
L2_REG = 0
MLP_HIDDEN_LAYERS = [64, 32, 16, 8]

# trainer config
OPTIMIZER = 'adam'
BATCH_SIZE = 64
EPOCHS = 30
VAL_SPLIT = 0.25

# load ratings
df_ratings = pd.read_csv(
    DATAPATH,
    usecols=['userId', 'movieId', 'rating'],
    dtype={'userId': 'int32', 'movieId': 'int32', 'rating': 'float32'})

# get total number of users and items
num_users = len(df_ratings.userId.unique())
num_items = len(df_ratings.movieId.unique())

# train/test split
df_train, df_test = train_test_split(df_ratings, TEST_SIZE, SEED)

# build Generalized Matrix Factorization (GMF)
GMF_model = get_GMF_model(num_users, num_items, EMBEDDED_DIM, L2_REG, L2_REG)

# build Multi-Layer Perceptron (MLP)
MLP_model = get_MLP_model(num_users, num_items, 
                          MLP_HIDDEN_LAYERS, [L2_REG for i in range(4)])

# build Neural Matrix Factorization (NeuMF)
NeuMF_model = get_NeuMF_model(num_users, num_items, EMBEDDED_DIM,
                              (L2_REG, L2_REG), MLP_HIDDEN_LAYERS, 
                              [L2_REG for i in range(4)])

# let's just train Neural Matrix Factorization (NeuMF)
train_model(NeuMF_model, OPTIMIZER, BATCH_SIZE, EPOCHS, VAL_SPLIT, 
            inputs=[df_train.userId.values, df_train.movieId.values], 
            outputs=df_train.rating.values,
            filepath=MODELPATH)

# load the best trained model
# rebuild
NeuMF_model = get_NeuMF_model(num_users, num_items, EMBEDDED_DIM,
                              (L2_REG, L2_REG), MLP_HIDDEN_LAYERS, 
                              [L2_REG for i in range(4)])
# # load weights
# NeuMF_model = load_trained_model(NeuMF_model, MODELPATH)

# define metric - rmse
rmse = lambda true, pred: np.sqrt(
  np.mean(
    np.square(
      np.squeeze(predictions) - np.squeeze(df_test.rating.values)
    )
  )
)

# test model
predictions = NeuMF_model.predict([df_test.userId.values, df_test.movieId.values])
error = rmse(df_test.rating.values, predictions)
print('The out-of-sample RMSE of rating predictions is', round(error, 4))
```