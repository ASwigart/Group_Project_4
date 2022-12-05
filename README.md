# Group_Project_4
Final Project for NU Data Analysis Bootcamp


Group Project 4:
Allie Carlile, Brevin Owens, Andrew Swigart 

Proposal: Using the Wine dataset from the UC Irving Machine Learning Repository, we propose to use machine learning to categorize the dataset into the 3\ different cultivars.\ At this point, we are not planning on creating a separate website. \We do plan to use pandas and matplotlib to complete the requirements. \We also plan to devlop this as the project develops.

https://archive-beta.ics.uci.edu/dataset/109/wine
  


Machine Learning:

The machine learning portion of the project took a step by step approach to categorize the dataset. First, I imported the csv file from the repository and created a dataframe. Then I created a scatter matrix and a heat map to see what the data looked like compared against itself. Since this dataset was complete and had previously been categorized the data cleaning aspect of the project was done for us. The heatmap accomplished the same visual analysis as the scatter matrix in a different way. Looking at both three candidates for correlations identified themselves, flavanoids, prolines, and total phenols, they all had right ward slopes.  Then I prepared the dataframe for machine learning. I took the type column and encoded it and set it as 'Y'. Then I used the 'train, test, split' to seperate the dataset. Specifically, I did an 80/20 split, shuffled the data to make it more random, and then used the stratify to ensure the training data was reflective of the total dataset. The original datset was sequential by class 1,2,3 in unequal amounts, so I tried to make the training set more random and reflective of the total data. Then I scaled the data using a standard scaler. The first pass gave us a training score of 97% and a testing score of 89%. Next I moved on to Known Nearest Neighbor analysis. Since we had 3 types of wine at the outset, the outcome was interesting. I ran it 3 times, at a range of 5, then 10, then 15. And the model struggled with the larger values. Once the curve moved past 3 the model struggled to find new neighbors. We just had a small dataset and the model returned a 1.0 f1 score in the classification report. It was not overfitted, it was just a small set with a small predetermined number of clusters. Next I did a simple feature importance analysis, which identified flavanoids, proline, & alcohol as the three most significant features in the dataset. Then a simple logisitic regression which had a weighted f1 score of 97%. Then a decision tree classifier, which also gave a 97% weight average f1 score. After a few false starts with bagging, I moved on to Ada Boost. Ada Boost the base model yielded a 92% weighted average. When I increased the estimators within the model from 100 to 200 to 200 with an increased learning rate, to 500, 1000, to 2000, the model did not surpass 92%. 



Neural Network: 

To start with the neural network model, I had to first split the wine data into features and target arrays. I then used a label encoder from the sci-kit learn preprocessing library to shape the target or type of wine correctly. This basically ensured that our neural network model knew that we were predicting 3 types of wine versus a binary model. From there I used the train test split function to separate the data into testing and training sets. I then used the standard scaler to scale the data appropriately before running any model. 


Clustering: 

To begin the clustering process, I plotted the raw data by flavanoid levels, alcohol levels, and type. It is illustrated in this plot that there are three definitive groups that may be clustered.

![image](https://user-images.githubusercontent.com/105824024/205749667-7c6a4551-f12d-4e4a-9ebe-397fd4ce773b.png)

The first technique I used was agglomerative clustering using the ward method. I first normalized the data and made a dendrogram where we can see three major hierarchical groups.

![image](https://user-images.githubusercontent.com/105824024/205751758-b37c0c22-6dbb-44b5-a447-3a3b5fde7b39.png)

I then plotted flavanoids and type using the normalized data with predicted clusters.

![image](https://user-images.githubusercontent.com/105824024/205752026-29f18083-b05c-43dd-886c-90266a0b3eb5.png)

Next, I used StandardScaler to scale and fit the original data and ran a principal component analysis. I transformed the PCA data using TSNE with a learning rate of 75 and plotted the TSNE features. There is a bit more visual clustering by type going on here. 

![image](https://user-images.githubusercontent.com/105824024/205752664-db8f98e8-c3e8-4c94-b06a-83f6944b8415.png)

Using KMeans, I created a for-loop to caculate the inertia for the range of k values in the PCA dataset. I made an elbow curve using hvplot, which shows that the curve begins to plateau around 3. 

![image](https://user-images.githubusercontent.com/105824024/205753785-508b009b-67f1-48ba-a91d-54039baa7c78.png)

After initializing and training the KMeans model, I created a return dataframe with the predicted clusters. This technique gave me the best visual result with three clear clusters. 

![image](https://user-images.githubusercontent.com/105824024/205754564-41c4afba-014e-4743-8f86-d5a5c555d2f2.png)




