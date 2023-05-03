---
title: Network analysis
prev: data-description
next: text-analysis
---

We construct the network based on the co-authorship of articles, to examine the collaborations of the news agencies.
We construct a graph where each node represents an author and each edge represents a co-authorship between two authors.
The network is undirected and unweighted. The size of the nodes are scaled based on the number of articles the author has written.
We create a graph for both Reuters and The New York Times.

In the image below the full New York Times graph can be seen.

![](/images/nyt0.png)

As can be seen there is a large blob in the center of the graph, containing a few authors with a larger number of articles,
and a lot of authors with a very small number of articles written, all belonging to the Movies section of the newspaper.
Upon further inspection we found that a majority of these "authors" were actually actors, actresses, or other celebrities
such as John Cena, Jake Gyllenhaal, Margot Robbie, etc. All of which had a low number of articles, where they were listed
as authors, likely due to the fact that they were the subject of the article or were interviewed for the article. As such we 
chose to remove all nodes with less than 5 articles written, and the corresponding articles that would result in having a 
single author or no author are also removed.

In the figures below we see the degree distribution of the largest connected component of New York Times graph before and
after removing the nodes with less than 5 articles written.

|               Before               |               After               |
|:----------------------------------:|:---------------------------------:|
| ![](/images/nyt_degree_before.png) | ![](/images/nyt_degree_after.png) |

Additionally, there are also some network statistics for the graph before and after removing these nodes.

|            Stat             |  Before  |   After   |
|:---------------------------:|:--------:|:---------:|
|           #Nodes            |  15,556  |   1,234   |
|           #Edges            |  79,857  |   7,342   |
|         Avg. degree         |  10.26   |   11.90   |
|        Median degree        |    7     |     5     |
| Avg. clustering coefficient |  0.792   |   0.184   |





The resulting graph of removing the nodes corresponding to authors with 5 or fewer articles written can be seen below.

![](/images/nyt1.png)

### Reuters randomization experiment

![](/images/reuters_mod.png)

### The New York Times randomization experiment

![](/images/nyt_mod.png)

|                          | Reuters                            | The New York Times                 |
|--------------------------|------------------------------------|------------------------------------|
| Section modularity       | 0.246                              | 0.239                              |
| Louvain modularity       | 0.547                              | 0.701                              |
| Randomization modularity | $$X\sim\mathcal{N}(0.016, 0.003)$$ | $$X\sim\mathcal{N}(0.030, 0.001)$$ |

From the randomization experiments we can see that although the section partitioning is quite a bit lower than the modularity than the partitioning
obtained by using the Louvain algorithm, but it is still significantly better than randomly partitioning the graph, which is what we would expect.


It is quite likely that the modularity of the Louvain partitioning of the New York Times graph is so high because of the 
large blob of nodes in the center of the graph, likely being assigned the same community by the algorithm. 
This is likely due to the fact that the blob is so densely connected that it is very hard to break it up into 
smaller communities.