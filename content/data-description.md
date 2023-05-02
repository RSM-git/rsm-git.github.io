---
title: Data description
prev: "/"
next: network-analysis
---
Our data consists of news articles from Reuters and The New York Times. We specifically chose to work with news articles as there is an apparent connection between a collaboration network of authors and text that they produce together.


The data used for this project is a subset of [All the News 2.0](https://components.one/datasets/all-the-news-2-news-articles-dataset/), which is an expanded version of the original All the News dataset.
All the News 2.0 contains 2,677,878 articles with the publications spanning from January 1, 2016 to April 2, 2020.

We chose to work with articles from the two publications with the most articles in the dataset: Reuters with 840,094 articles, and The New York Times with 252,259 authors.

After preprocessing which includes removing data points with missing entries, we are left with 59,600 articles from Reuters and 28,511 articles from The New York Times.

Each article has a section attribute which allow us to get an overview of which topics are most important to the two publications
![](/images/reuters_top_5_sections.png)

![](/images/nyt_top_5_sections.png)
