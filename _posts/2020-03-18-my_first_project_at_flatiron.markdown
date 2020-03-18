---
layout: post
title:      "My first project at Flatiron."
date:       2020-03-18 11:44:29 -0400
permalink:  my_first_project_at_flatiron
---



For our first project Flatiron, we were tasked with analyzing movie content and to recommend what type of movie for Microsoft to focus on.  Since this was our first project, it was basic exploratory data analysis but I think it was a good first project to get my feet wet.


# Project description
Microsoft was noticing that these other big companies were making their own original content and wanted in on the game.  They asked us to review movie data and recommend the best type of movie to work on.  I chose a movie dataset off kaggle.com with over 5,000 records.  Some of the columns included the production budget, the gross profit, the studio that made the movie and the rating.



# My process
I first imported the data into a dataframe with pandas to check the column names.  I chose the columns that I thought would have the biggest affect on profit.  I kept trying to graph profit but I soon realized I had to change the data type to an integer for it to be graphed. I first wanted to check the average runtime for any given movie using a histogram and found the average movies were 90 minutes long.  I then made a separate table using pd.crosstab to count the number of occurences there were for each movie in the dataset.  Action, Adventure, and Animation appeared the most with 1331, 392, 277 occurences respectively and then plotted it using matplotlib.  I made a separate dataframe using this new information `movies = movies[['genre', 'budget', 'profit', 'runtime', 'rating', 'company', 'director', 'year']]
movies.sort_values(by=['profit', 'budget'], ascending=False, inplace=True) and sorted profit and budget in descending order.  I then wanted to check both profit based on genre and budget based on genre using a bar chart in seaborn sns.catplot(x='genre', y='profit', data=Top_movies, kind='bar', aspect=3 ) sns.catplot(x='genre', y='budget', data=Top_movies, kind='bar', aspect=3 ).  I sliced the dataframe further into the top 5 movies and graphed those based on profit and out of those action was the most profitable followed by drama.




# Recommendation

Based on the dataset I used and from my analysis I recommend an action PG-13 movie that's around 90 minutes long.  I think another important consideration is the usual viewer of the movie, when the movie is released and the star actor of that movie.

