## Anime Recommendation System
Matt Carey, Kai Hansen, Paula M-Bailey, Steve Njoroge, and Mohammed Qurneh
=======================

## **Introduction**

With humble beginning that trace to late 19th century Japan, Anime has become global phenomenon captivating audiences.  As the number of titles grows, discovering new titles can be overwhelming.  This is where an anime recommender system can be beneficial.  

Our aim is to design a system to enhance the user’s experience by suggesting relevant shows and movies based on their taste and behavior patterns.  By analyzing viewer history, ratings, and behavior, we can identify patterns and similarities that could lead users to new titles. 

In this project, we focused on  building a content-based recommendation system. This system generates suggestions based on content that another user has previously enjoyed.  By using cosine similarity, we can compare features and identify those that match a user's interest and taste.  The goal is to create a way for users to discover new anime.  To evaluate the success of our recommendation system, we will test it out with members of our team and classmates.


## **What is a Recommendation System?**

A recommendation system is an algorithm designed to suggest relevant products to a user based on the user’s behaviors, similarities with another user, and interests.  Products can include books, music, videos, travel destinations, friends and connections, etc.


## **How does it work?**

It begins with access to user data. Next, a content-based matrix is created based on the viewed anime titles and their ratings. A weighted feature matrix is computed using the user's matrix and the matrix containing all titles. This weighted features matrix is calculated using a similarity algorithm like cosine similarity, which determines how similar two vectors are to one another. The formula is as follows:

<!DOCTYPE html>
<html>
<head>
  <script type="text/javascript" async
    src="https://cdnjs.cloudflare.com/ajax/libs/mathjax/3.1.2/es5/tex-mml-chtml.js">
  </script>
</head>
<body>

<p>Cosine Similarity \( x, y = \frac{x \cdot y}{||x|| \cdot ||y||} \)</p>

<p>where:</p>
<ul>
  <li> \( x \cdot y \) is the dot product of vectors \( x \) and \( y \)</li>
  <li> \( ||x|| \) is the magnitude (norm) of vector \( x \)</li>
  <li> \( ||y|| \) is the magnitude (norm) of vector \( y \)</li>
</ul>

</body>
</html>




It measures the cosine of the angle between the vectors and produces a value between -1 and 1. A value of 1 suggests that 𝑥 and 𝑦 are very similar in tastes. A value of 0 suggests that 𝑥 and 𝑦 don’t share any interests, while a value of -1 suggests that 𝑥 and 𝑦 have opposite interests.

## **The Data**
This project contains two datasets, one with the anime rating and the other with information escribing the anime itslef.  Both datasets is located here. **Link is Weird includes Kai repo** []("https://www.kaggle.com/datasets/CooperUnion/anime-recommendations-database?select=rating.csv") from Kaggle.

User data contains 7.8 million entries of user ratings.

Includes:
- user id 
- anime title  
- rating

Anime Data contains 12,200 entries describing anime shows and movies.

Includes:
- The title of the anime.
- The associated genres (e.g., action, comedy, drama).
- Whether it’s a TV show or a movie.
- The number of episodes.
- The overall average rating and popularity based on how many users rated it.

## **Pre-Processing**
