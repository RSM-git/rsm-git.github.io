---
title: Project Summary
layout: single
next: data-description
---

# **What is this project about?**

DISCLAIMER: ALL STATEMENTS ARE BASED SOLELY ON THE SUBSET OF DATA THAT WE HAVE CURATED AND ARE NOT UNBIASED. See the *Data* page for a discussion of biasses.

In this project we have analyzed the collaboration between authors within the news agencies Reuters and The New York Times.

# **Data**

The data used to perform the analysis is a collection of articles, called [All The News 2.0](https://components.one/datasets/all-the-news-2-news-articles-dataset/) 
which has been scraped from the web. The dataset contains articles from most American news agencies, with the two largest being Reuters and The New York Times.

The data was pre-processed to remove articles with essential missing information, such as author, section or article text, as well as 
filtering the authors to only include those who have written at least 5 articles to remove potential outliers.


# **Networks**

Using the processed data we constructed an undirected and unweighted collaboration graph for each of the two news agencies. 
In the graph each node represents an author and an edge between two nodes represents a collaboration between the two authors.
We chose to look at the largest connected component of each graph, as very few nodes were disconnected from the main component.

The graphs were partitioned using the section feature of the articles, by assigning each node a community based on the section in which the author has written the most articles.
The section partitioning was compared with a partitioning based on the Louvain algorithm, as well as a random partitioning of the graph.

The modularity experiments showed that the section partitioning of the New York Times graph, was similar to the partitioning based on the Louvain algorithm,
while the section partitioning of the Reuters graph was quite a bit different from the Louvain partitioning, but still significantly better than the random partitioning.


# **Text analysis**

Using the processed data we separated the articles from the two agencies by section. With the articles categorized by section, we did a Term Frequency (TF) and Term Frequency inverse Document Frequency (TF-IDF) on the articles. Doing so allowed us to compare the two agencies' use of terms in similar sections.

From the Tf-IDF we found that in particular the NYT section "US" and the Reuters section "Politics" seemed similar in terms of word usage. With this in mind, we ran a Sentiment analysis on all the articles from their respective agencies. Here we found that the news agencies tend to be predominantly negative in their coverage, at least in the dataset that we have.


To see the fully detailed analysis with code, please see the explainer notebook linked below.
# [Explainer Notebook](explainer-notebook.html)