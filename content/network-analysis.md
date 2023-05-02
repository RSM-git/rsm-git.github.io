---
title: Network analysis
prev: data-description
next: text-analysis
---

We construct the network based on the co-authorship of articles. We define two authors as co-authors if they have
written at least one article together. We then construct a network where each node represents an author and each edge
represents a co-authorship between two authors. The network is undirected and unweighted. The nodes are scaled based on
the number of articles the author has written. A network is created for each publication.

In the image below the full Reuters graph can be seen.

![](/images/reuters0.png)

As can be seen, the largest connected component of the graph is surrounded by a large number of small components. We
chose to focus on the largest component as there are not many connections to investigate in the smaller components.
Where the nodes are colored based on the author's most publicised section in the dataset.

![](/images/reuters1.png)

In the following image the Reuters graph is shown with the nodes colored based on the Louvain community detection
algorithm.

![](/images/reuters2.png)

The New York Times graph is shown below, we see that there is a very large blob in the center of the graph,
containing a few big authors and majorly authors with a small number of articles written.
Most if not all of these authors belong to the "Movies" section of the newspaper, and are likely to be actors,
actresses, directors, etc. such as John Cena, Jake Gyllenhaal, etc.

![](/images/nyt0.png)

Akin to the Reuters graph, there were a lot of small components surrounding the largest component. And we once again
chose to focus on the largest component.
With the nodes being colored based on the author's most publicised section in the dataset.

![](/images/nyt1.png)

And once again the graph is shown with the nodes colored based on the Louvain community detection algorithm.

![](/images/nyt2.png)

For both of the graphs we perform randomization experiments using the double edge swap algorithm and computing the
modularity of the randomized graphs using the section partitioning of the graph.

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