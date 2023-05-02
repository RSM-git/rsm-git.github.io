---
title: Network analysis
prev: data-description
next: text-analysis
---

We construct the network based on the co-authorship of articles. We define two authors as co-authors if they have written at least one article together. We then construct a network where each node represents an author and each edge represents a co-authorship between two authors. The network is undirected and unweighted. The nodes are scaled based on the number of articles the author has written. A network is created for each publication.

In the image below the full Reuters graph can be seen.

![](/images/reuters_full_graph.png)

As can be seen, the largest connected component of the graph is surrounded by a large number of small components. We chose to focus on the largest component as there are not many connections to investigate in the smaller components.
Where the nodes are colored based on the author's most publicised section in the dataset.

![](/images/reuters_graph.png)

In the following image the Reuters graph is shown with the nodes colored based on the Louvain community detection algorithm.

![](/images/reuters_louvain_graph.png)

The New York Times graph is shown below, we see that there is a very large blob in the center of the graph,
containing a few big authors and majorly authors with a small number of articles written.
The large majority of these authors have the section "Movies", examining the authors of the "Movies"
section we see that a lot of these "authors" are most likely actors and actresses that have been interviewed.

![](/images/nyt_full_graph.png)

Akin to the Reuters graph, there were a lot of small components surrounding the largest component. And we once again chose to focus on the largest component.
Where the nodes are colored based on the author's most publicised section in the dataset.

![](/images/nyt_graph.png)

And once again the graph is shown with the nodes colored based on the Louvain community detection algorithm.

![](images/nyt_louvain_graph.png)