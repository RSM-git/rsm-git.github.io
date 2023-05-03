---
title: Data description
prev: "/"
next: network-analysis
---
The data used for this project is a subset of [All the News 2.0](https://components.one/datasets/all-the-news-2-news-articles-dataset/), which contains 2,677,878 news articles American publications spanning from January 1, 2016 to April 2, 2020.

We chose to work with articles from the two publications with the most articles in the dataset: Reuters with 840,094 articles, and The New York Times (NYT) with 252,259 authors.

The dataset contains 10 features: authors, title, article text, url, section, publication and four features describing the time of publication.
The features used in this project are: authors, article text, and section. 

# Preprocessing
While the data is plentiful, a lot of samples are missing entries or has otherwise corrupted entries. 
To discard these samples, we took the following preprocessing steps
1.  Remove articles not from Reuters or The New York Times
2.  Remove articles that are missing either author, section or article
3.  Remove articles in sections that has fewer than 100 articles
4.  Remove authors that has written fewer than 5 articles
5.  Remove articles that has fewer than 2 authors

The preprocessing steps are important to describe since they bias the data and thereby the analysis.
In this project we are thus only concerned with articles from the biggest sections of each publication that furthermore is written by at least two authors. These steps discard a signifant part of the dataset especially since most articles are written by a single author thus, the subset of data that we have currated is not an unbiased subset of articles.

The major reason for removing authors with fewer than 5 articles is that the NYT data had celebrities noted as authors for several articles but this preprocessing step discarded most of these articles. See the explainer notebook for all the details.

# Statistics
After preprocessing the data, we end up with substantially fewer articles as seen in the summary statistics table below

|            Stat             |  Reuters  |   NYT   |
|:---------------------------:|:--------:|:---------:|
|           #Articles            |  56,046  |   24,377   |
|           #Sections            |  39  |   21   |
|         #Authors         |  1,952   |   1,287   |
|        Avg. words pr. article        |    608     |     1094     |
|        Avg. #articles pr. author        |    29     |     19     |

Each article has a section attribute which allow us to get an overview of which topics are most important to the two publications
![](/images/reuters_top_5_sections.png)

![](/images/nyt_top_5_sections.png)
