##Introduction
Some of our strongest geographic and cultural associations are tied to a region's local foods. This project is mainly to apply different classifier to predict the category of a dish's cuisine given a list of its ingredients and figure out the relationship between them. This would be a great help to the food market or food distributor. They can interpret the ingredient list and better arrange the food in their market. It can also help the consumer to better understand relationship between different cuisines and pick restaurant they may like.

##Data acquisition
The data we use is provided by”Yelp”, which includes 39774 recipes. These recipes can be classified into 20 types of cuisines, and there are 6174 different ingredients in all these recipes.  I pick 75% of the data to train and 25% to test. 

##Result
###Word2Vec
Firstly, I use word2vec to project each ingredient to a 600 dimension space. I tested word2vec prepared dataset with KNN, SVM with rbf kernel and logistic regression and one hidden layer neural network. ![](https://github.com/danwang123/Cusine_Prediction/blob/master/Images/word2.jpeg?raw=true)
###Bag of words
Instead of considering the interactions, a more straightforward method to prepare data is bag of world. We set each ingredient as an independent vector so every recipe would be a 6714 dimension vector. Applying SVM with rbf kernel, random forest and logistic regression, we find out the accuracy of each classifier is more than 70%. This means the bag of word has better performance than word2vec, so the interactions between ingredients may be not significant as what we thought.

###![](https://github.com/danwang123/Cusine_Prediction/blob/master/Images/bow.jpeg?raw=true)
From figure 4 we can find that logistic regression has the best performance. To further improve the performance, we implement some high correlation combinations from all cuisines.

###![](https://github.com/danwang123/Cusine_Prediction/blob/master/Images/threshold.jpeg?raw=true)

###Network in Cuisine
Apart from accuracy we also want to know the relationship between different cuisines. So that we calculated the cosine similarity and visualize the relationship. 
First, we directly calculated the cosine similarity between the vectors from bag of word, with each ingredient equally treated. 

###![](https://github.com/danwang123/Cusine_Prediction/blob/master/Images/data_vis.jpeg?raw=true)

We can tell from these graphs that it’s very hard to separate different cuisines. In order to make some improvement we embed the coefficients that we get from logistic regression as the weight for each ingredients. This adjustment led to a dramatic improvement in the result.

###![](https://github.com/danwang123/Cusine_Prediction/blob/master/Images/data_vis_cof.jpeg?raw=true)

We can see from these weight plot that it’s easy to separate cuisines which are quite different, such as British and Chinese cuisines. Also those cuisines who have more commons will stay closer. We can tell from the graph of British, Japanese and Chinese Cuisine that British Cuisine are obviously separated from the other two, which have more common and are both Asian Cuisine. Also we got some interesting results, for example, we found that Korean food is closer to Jamaican food rather than Japanese food which is also from Asia.

