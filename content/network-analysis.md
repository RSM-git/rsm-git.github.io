---
title: Network analysis
prev: data-description
next: text-analysis
---

We construct the network based on the co-authorship of articles, to examine the collaborations of the news agencies.
We construct a graph where each node represents an author and each edge represents a co-authorship between two authors.
The network is undirected and unweighted. The size of the nodes are scaled based on the number of articles the author has written.
We create a graph for both Reuters and The New York Times.

## **The New York Times**

In the image below the full New York Times graph can be seen.

![](/images/nyt0.png)

As can be seen there is a large blob in the center of the graph, containing a few authors with a larger number of articles,
and a lot of authors with a very small number of articles written, all belonging to the Movies section of the newspaper.
Upon further inspection we found that a majority of these "authors" were actually actors, actresses, or other celebrities
such as John Cena, Jake Gyllenhaal, Margot Robbie, etc. All of which had a low number of articles, where they were listed
as authors, likely due to the fact that they were the subject of the article or were interviewed for the article. As such we 
chose to remove all nodes with less than 5 articles written, and the corresponding articles that would result in having a 
single author or no author are also removed.

The resulting graph of removing the nodes corresponding to authors with 5 or fewer articles written can be seen below.

![](/images/nyt1.png)

There are some nodes which are disconnected from the main component, and as such will not be able to give much information
about the community structure of the graph. As such we choose to look at the largest connected component, which holds the majority
of the nodes in the graph. In the figures below we see the degree distribution of the largest connected component of New York Times graph before and
after removing the nodes with less than 5 articles written.

|               Before               |               After               |
|:----------------------------------:|:---------------------------------:|
| ![](/images/nyt_degree_before.png) | ![](/images/nyt_degree_after.png) |

Additionally, there are also some network statistics of the largest connected component of the graph before and after removing the unwanted nodes.

|            Stat             |  Before  |   After   |
|:---------------------------:|:--------:|:---------:|
|           #Nodes            |  15,556  |   1,234   |
|           #Edges            |  79,857  |   7,342   |
|         Avg. degree         |  10.26   |   11.90   |
|        Median degree        |    7     |     5     |
| Avg. clustering coefficient |  0.792   |   0.184   |

The largest connected component of the processed New York Times graph can be seen below.

![](/images/nyt2.png)

The Louvain community detection algorithm was used on the largest connected component of the graph giving the following partitioning of the graph.

![](/images/nyt3.png)

There are some differences between the partitioning given by the authors' most common section and the partitioning given by the Louvain algorithm, 
but also a lot of similarities.

We computed the modularity of both partitions and performed a randomization experiment to see if the modularity of the partitions are
significantly better than a random partition of the graph. The randomization experiment was performed by using the double edge swap
algorithm and calculating the modularity of the resulting partition. This was done 500 times, the resulting distribution along with the
modularity of the section and Louvain partitions can be seen in the figure below

![](/images/the_new_york_times_graph_mod.png)

In the table below the modularities from the two partitions and the randomization experiment can be seen for the New York Times graph.

|  Section  |  Louvain  |         Randomization         |
|:---------:|:---------:|:-----------------------------:|
| $$0.460$$ | $$0.515$$ | $$\mathcal{N}(0.003, 0.004)$$ |

## **Reuters**

Like with the New York Times graph authors with less than 5 articles written were removed, and articles that would have no or a single author were also removed.

The graph prior to removing any nodes can be seen below, with the nodes scaled based on the number of articles written by the 
author and colored based on the author's most published section.

![](/images/reuters0.png)

The New York Times graph had a lot of nodes representing non-authors, this was much less of a problem for the Reuters graph, 
but we still chose to remove the nodes with less than 5 articles written, this was done to remove possible anomalies in the data. 
The resulting graph can be seen below.

![](/images/reuters1.png)

The network statistics of the graph before and after pruning can be seen in the table below.

|            Stat             | Before | After  |
|:---------------------------:|:------:|:------:|
|           #Nodes            | 3,276  | 1,942  |
|           #Edges            | 19,071 | 14,943 |
|         Avg. degree         | 11.64  | 15.39  |
|        Median degree        |   4    |   10   |
| Avg. clustering coefficient | 0.220  | 0.269  |

Once again we chose to look at the largest connected component of the graph, which can be seen below.

![](/images/reuters2.png)

And the partitioning of the largest connected component of the graph given by the Louvain algorithm can be seen below.

![](/images/reuters3.png)

To compare the partitioning given by the Louvain algorithm and the section partitioning the modularity of each partition was
computed and a randomization experiment was performed akin to the one performed on the New York Times graph.

![](/images/reuters_graph_mod.png)

The modularity of the two partitions and the randomization experiment can be seen in the table below.

|  Section  |  Louvain  |         Randomization         |
|:---------:|:---------:|:-----------------------------:|
| $$0.242$$ | $$0.558$$ | $$\mathcal{N}(0.014, 0.003)$$ |


Comparing the two graphs we see that the modularity of the section partition in the Reuters graph is quite a bit lower than the Louvain partition, 
whereas the modularity of the section partition in the New York Times graph is much closer to that of the Louvain partition. 
This could be due to the fact that the collaboration within the New York Times is mostly between authors of the same section,
whereas the collaboration within Reuters is more spread out across sections. This is likely due to the fact that there are fewer sections
in the New York Times covering a wider range of topics, having articles from 21 unique sections, being partitioned into 13 communities by the Louvain algorithm.
Whereas Reuters has more sections covering more specific topics across 39 sections partitioned into 14 communities by the Louvain algorithm.


