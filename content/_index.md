---
title: Project Summary
layout: single
next: data-description
---

DISCLAIMER: ALL STATEMENTS ARE BASED SOLELY ON THE SUBSET OF DATA THAT WE HAVE CURATED AND ARE NOT UNBIASED. See the [data](data-description) page for a discussion of biasses.

To see the fully detailed analysis with code, please see the explainer notebook linked below.
# [Explainer Notebook](explainer-notebook.html)

# **What is this project about?**
In this project we have analyzed how authors collaborate within Reuters and The New York Times (NYT) both in terms of who they are writing with and how they are writing.

# **Data**
The data used to perform the analysis is a collection of articles, called [All The News 2.0](https://components.one/datasets/all-the-news-2-news-articles-dataset/) 
which has been scraped from the web. The dataset contains articles from most American news agencies, with the two largest being Reuters and The New York Times.

After preprocessing, we were left with about 57,000 articles from Reuters, and 24,000 articles from the NYT.

The five sections with the most articles are shown below
<img src="/images/reuters_top_5_sections.png" alt="drawing" width="600"/>
<br></br>
<img src="/images/nyt_top_5_sections.png" alt="drawing" width="600"/>


See the [data](data-description) page for more details about the dataset.

# **Networks**

Using the processed data we constructed an undirected and unweighted collaboration graph for each of the two news agencies. 
In the graph each node represents an author and an edge between two nodes represents a collaboration between the two authors.
We chose to look at the largest connected component of each graph, as very few nodes were disconnected from the main component.

The graphs were partitioned using the section feature of the articles, by assigning each node a community based on the section in which the author has written the most articles. Nodes with the same colours are authors with the same section.
The NYT network:

TODO: SMALL TABLE WITH 
COLOR : SECTION
![](/images/nyt2.png)

The NYT network shows that there are two major components: the larger one with several sections, and a smaller one to the left with only authors of the same section. The nodes in the smaller component are all authors from the movie section and shows how they very rarely collaborate with authors outside of their own section.
The larger component is more mixed but it's still clear that authors from the same section are grouped together.

![](/images/reuters2.png)
The reuters network is way more mixed showing that authors are more likely to collaborate with other authors from different sections but there are still clear tendencies such the red nodes being exclusively on left half of the graph.

These visual interpretations are backed up by looking at the modularity with regards to section

<img src="/images/the_new_york_times_graph_mod.png" alt="drawing" width="600"/>
<br></br>
<img src="/images/reuters_graph_mod.png" alt="drawing" width="600"/>

These graphs show us that the section modularity is about 0.5 for the NYT but only around 0.2 for Reuters. However, both of these modularities are significantly higher than the modularities of the randomization experiments with the double edge swap algorithm. These results confirm that authors from both publications are more likely to write with authors from the same section and that this is more so the case for the NYT than Reuters.
See the [network](network-analysis) for more details.

# **Text analysis**
For the text analysis, we started with looking at word clouds generated with tf-idf for each section of the two publications.
Since we wanted to compare how the publications portray the same subject, we looked for the sections which were mostly related with the 2016 US presidential election as we expected this to be the subject of numerous articles due to the time period in which the dataset was currated.
We found that the us sections of the NYT and the politics section of Reuters seemed to have the most emphasis on the election based on the following word clouds

<img src="/images/Reuters_TFIDF_Politics.png" alt="drawing" width="600"/>
<br></br>
<img src="/images/NYT_TFIDF_us.png" alt="drawing" width="600"/>


The word clouds are in fact so simillar that it is very difficult to discern any difference at all and as such we can only conclude that we *can not* find any difference in their writing style from the word clouds alone. This is not a fault of word clouds since they are excellent at depicting the central topics, they are just not great at discerning *how* the articles are written.

Instead we will use sentiment analysis with transformer models which are great at capturing opinionated writing but they only distinguish between three categories: negative, neutral, and positive, which is of course a great simplification of writing.

The table belows shows the number of articles with a given sentiment for the two sections that we are focusing on.
|                                     |               Reuters politics section              |               NYT us section               |
|:----------------------------------:|:----------------------------------:|:---------------------------------:|
|Negative | 2,472 (81%) | 5,938 (76%)|
|Neutral | 353 (12%)| 1,118 (14%)|
|Positive | 212 (7%)| 771 (10%)|

We see that both newspapers have a very negative sentiment with Reuters being the most negative at 81%!
Perhaps the state of US Politics has left the authors utterly distraught and left them no choice but to write negative and opionated articles?
Well, looking at the sentiment of all the articles in the dataset, it seems that it's not the section that has a negative tone but the publications as a whole.
|                                     |               Reuters               |               NYT               |
|:----------------------------------:|:----------------------------------:|:---------------------------------:|
|Negative | 47,651 (83%) | 17,376 (73%)|
|Neutral | 5,812 (10%)| 3,384 (14%)|
|Positive | 3,666 (7%)| 3,036 (13%)|

We believe that these results are caused by the well known phenomenon that [the average person is drawn to negative news](https://www.bbc.com/future/article/20140728-why-is-all-the-news-bad) and ultimately publications print what sells.

To see more details, head over to the [text](text-analysis) section.

# **Conclusion**
In conclusion, we have found that for both publications, authors tend to collaborate with authors within their own section but that this more common at the NYT than at Reuters.
We also discovered that the publications write in a very negative sentiment and that we from our analysis did not find any indication of political bias. However, these are purely the results of the tools that we have used which we have found are clearly not well suited for the task, so all we say is that the sentiment of the articles does not seem to be affected by the section they are written in but rather as a result of how most articles are written in today's age.
