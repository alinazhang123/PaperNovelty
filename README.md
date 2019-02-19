# PaperNovelty - Identify the novelty of research papers

Question: Given a recently published paper (from 2016 onwards), is there a set of papers from 1990-2015 that are closely related to it?

Introduction
To address this question, I mainly focused on the abstracts of papers, which carries rich information that summarizes the papers.

To explore the data set, I first employed the topic modeling technique LDA to explore the topics of the training datasets. I then applied the trained LDA model onto the testing dataset to examine the similarity of topics across the two datasets.

By employing the word embedding model word2vec, I converted all the abstract texts into vectors of 300 features each. I then conducted a K-means clustering analysis on all the abstract vectors. The combination of the word embedding and the clustering methods allowed me to extract various semantic categories the papers belong to. The number of clusters used in the analysis was in consistency with the pre-defined number of topics used in the LDA topic modeling.

Next I conducted a PCA analysis to reduce the dimentionality of the 300-dimensional abstract vector space down to 3 components. The K-Means labels previously obtained were used to visualize the distributions of the papers across different PCA components. I validated my approach by applying the PCA and K-Means modeling to the validation dataset to visually verify the goodness of the clusters.

Finally, I picked a random paper from the testing dataset and checked whether there is a set of papers from the training dataset that are closely related. To do that, I calculated the similarity score between the example paper and all other papers that belong to the same KMeans cluster. I was specifically interested in those papers with a similarity score greater or equal to 0.90.

My pipeline is listed below.

Pipeline

Get data ready: Data import and visualization
Data exploration -- Topic modelling using LDA: Three topics were pre-defined (training and testing data)
Word2vec: Used a pre-trained model for converting each abstract in the training and testing dataset into vectors
Kmeans clustering:
Used to cluster the paper abstracts in the training dataset into different categories (training data)
Predicted the testing data based on the K-means model from the training dataset (testing data)
PCA
Reduced the data dimentionality from 300 features to 3 PCA components (training data)
Validated the model by applying the same PCA transformation from the training dataset to the testing and validation datasets (testing & validation data)
Plotted the data across the PCA components using K-means labels
Similarity scores
Calculated the cosine similarity scores between a randomly selected paper and all other papers within the same K-means cluster
Identified whether there is a set of papers that show close semantic similarity with the given paper
