Anime Recommendation System
=======================
Matt Carey, Kai Hansen, Paula M-Bailey, Steve Njoroge, and Mohammed Qurneh

## **Introduction**

With humble beginning that trace to late 19th century Japan, Anime has become global phenomenon captivating audiences.  As the number of titles grows, discovering new titles can be overwhelming.  This is where an anime recommender system can be beneficial.  

Our aim is to design a system to enhance the user’s experience by suggesting relevant shows and movies based on their taste and behavior patterns.  By analyzing viewer history, ratings, and behavior, we can identify patterns and similarities that could lead users to new titles. 

In this project, we focused on  building a content-based recommendation system. This system generates suggestions based on content that another user has previously enjoyed.  By using cosine similarity, we can compare features and identify those that match a user's interest and taste.  The goal is to create a way for users to discover new anime.  To evaluate the success of our recommendation system, we will test it out with members of our team and classmates.


## **What is a Recommendation System?**

A recommendation system is an algorithm designed to suggest relevant products to a user based on the user’s behaviors, similarities with another user, and interests.  Products can include books, music, videos, travel destinations, friends and connections, etc.


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

Out of the 7.8 million reviews, we see no null values are present, meaning we do not need to remove any observations.  Next, we split our genre into 3 separate features, capturing the first 3 genres assigned to the specific anime piece. As part of the pre-processing step, we will want to remove outliers in our datasets. This is because outliers weigh and skew the recommender system to produce less than optimal results. Another critical part of the pre-processing step is to convert the object data into integer values that our system can read. Using the OneHotEncoder, we can create a list of 0's and 1's, assigning the label depending on whether the feature has the specific object or not. For example, let’s say we Action, Comedy, Drama, the OneHotEncoder turns genre_1 into [Action, Comedy, Drama] then into [1, 0, 0] for if the feature has it or not. That list there would show the data's genre for genre_1 would have an action label. This allows for a readable version for our recommender system. Finally, we standardize our features. This is important, because unstandardized features could allow for larger weights and create heavier pulls for features that should not have it. By standardizing, we put all features on an even playing field and allow each individual feature to uniquely express itself.

<img src="images/Pix1.png" alt="Description" width="600" height="600" />

This shows the distribution of ratings, members, ways the anime is shown, and distribution it is shown. For the ratings, we see that majority of the ratings are around a 7, with there being higher and lower ratings. This gives a baseline at potentially the sort of rating we expect to use to recommend to the user. With majority being 6 or higher, its highly unlikely that our system may recommend a piece that is rated less than that. As for distribution of members, we see a majority of anime pieces have a smaller viewer audience. For distribution of episodes, we see that while larger pieces exists, majority hang around 100 or less, indicating majority of users and pieces do not create and enjoy larger amounts of episodes. As for the distribution of type of showing, we see the majority of viewers enjoy either movies, TV series or original video animations (Anime shown straight to home through things like VCRs in the 80's, as opposed through a TV channel or movie theater)

<img src="images/Pix2.png" alt="Description" width="600" height="650" />

This shows the top 10 anime titles viewed by users.

## **Modeling**
### Cosine Similarity

It begins with access to user data. Next, a content-based matrix is created based on the viewed anime titles and their ratings. A weighted feature matrix is computed using the user's matrix and the matrix containing all titles. This weighted features matrix is calculated using a similarity algorithm like cosine similarity, which determines how similar two vectors are to one another. The formula is as follows:

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

### Feature Selection
Features used to calculate similarity:
- Type
- Number of Episodes
- Average Rating
- Popularity
- Genres previouslyPrimary, Secondary and Tertiary

A similarity matrix was generated where each anime is compared to every other anime based on the above features
	
Recommendation Strategy
For each user:
- Identify anime they rated 7 or above.
- Find the 5 most similar anime for each highly rated title.
- Rank suggestions to create a list of the top 5 recommendations


## **Evaluation Metrics**
Coverage: 37%
- The percentage of anime titles that appear in at least one user’s recommendation.
- Indicates the system recommends a moderate portion of the total available titles.

Diversity: 0.22
- Measures how dissimilar the recommended items are within a user’s list.
- Suggests the recommendation are  highly similar to one another.
- Indicates a bias toward popular genres

Insights
- The system successfully generates recommendations but favors popular genres and lacks variety.
- Improving diversity and expanding coverage to niche titles would enhance system performance.


## **Impacts**
Positive Impacts
Enhanced User Experience:
- Provides personalized recommendations based on user viewer history
- Introduces users to new titles and expands their interests.
Merchandising and Revenue Growth:
- Promotes engagement with specific genres or franchises, supporting merchandise sales.
- Encourages further exploration within the app, increasing subscription retention.
Time-Saving and Community Engagement:
- Saves users time by curating relevant content.
- Builds engagement among users within the community and subscription base.


Negative Impacts
- Reduced variety by recommending similar titles repeatedly may limit exposure to new, diverse content.
- User isolation since heavy reliance on personalized services may lead to increased isolation and reduced social interaction.


## **Conclusion**
From our recommendery system, we see that we were able to successfully create a system that can highlight potential pieces of anime for a viewer. To test this out, it would be good to actually look at the recommended pieces of anime this system would give for you individually, and see if you like its recommendations. There were some issues though with the system, which we believe come from the data. The coverage of anime pieces and diversity of recommendations was not as high as one may like. This could be for a large range of factors, but based on the visualization, we can paint a picture why. When looking at our recommendations, we saw high amounts of products that contained genres with action, comedy, adventure, drama, and fantasy. Yet is saw very small representation in genres such as cars, vampires, and super powers. By having such large and potentially over-represented pieces, our system forms a bias against these other pieces, especially when ratings are factored in. Now, this could be normal as well. Its possible that the anime community as a whole does not value those latter genres. To make the recommender system more accurate and potentially cover more pieces, it would be good to collect larger datasets with wider range of genres covered, for the system to get a better understanding. But playing the other side of the coin, it could also be possible that are system is catching a trend in what genres people enjoy viewing, and signal what genres should potentially not be created in high demand.