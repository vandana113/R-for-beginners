
# GGPlot2

### 1. Read the 'MovieRating.csv' into the dataframe called 'movies' 

```R
movies <- read.csv("MovieRating.csv")

#See the structure of 'movies' using str()
str(movies)
#'Genre' is categorical variable/column but 'year' is treated as non-categorical variable 

#We want to treat it as categorical variable , so this is done by using factor() function
movies$Year <- factor(movies$Year)
#Now 'Year' is a factor with 5 levels(2007,2008,2009,2010,2011)

```

### 2. Scatter Plot(with smoothing) to compare AudienceRating v/s CriticRating

```R
q <- ggplot(data = movies , aes(x=CriticRatings,y=AudienceRatings,
                                color = Genre,size = BudgetMillion))
#Here we are mapping the color to genre , so it is put inside the aesthetics function called aes()

h <- q + geom_point(size=1.5,alpha=0.5) + geom_smooth(fill=NA,
                                     size=1.25)

#Adding themes
h + ggtitle("Audience  Rating v/s Critic Rating") +
  theme(axis.title.x = element_text(size=20,color = "Red"),
        axis.title.y = element_text(size=20,color = "DarkBlue"),
        axis.text.x = element_text(size = 10),
        axis.text.y = element_text(size = 10),
        plot.title = element_text(size = 30,color = "DarkGreen",family="Courier"),
        plot.background = element_rect(fill = "LightCyan", color = "Black"),
        legend.position = c(0,1),
        legend.justification = c(0,1)
  ) +
  coord_cartesian(ylim=c(10,100))

```

  #### Result
  ![Scatter Plot showing AudienceRating v/s CriticRating](https://github.com/kawal2266/R-for-beginners/blob/master/Plotted%20Graphs/aud_critic.png)

  #### Conclusion

> The purple line shows Romance Genre and it is clear that even when the Romantic movie is rated very low by the Critics (25) , even though it is liked by the Audience.
> For Action Genre ,  Audience and Critic shows the similar behaviour.You must have a good plot to impress the audience :wink:
> (Blue and Pink line)And for high Critic-Rating for Horror and Thriller , Audience choose Thriller over Horror. Horror Movie's business is risky :disappointed_relieved:

### 3. AudienceRating v/s Film's Budget 

```R
j <- ggplot(data=movies , aes(x=BudgetMillion,y=AudienceRatings,
                              color=Genre,size=BudgetMillion)) + 
  ggtitle("Audience-Rating v/s Budget of the Film") +
  theme(
    axis.text.x = element_text(size=10,color="Black"),
    axis.text.y = element_text(size=10,color="Black"),
    axis.title.x = element_text(size=15,color="DarkBlue"),
    axis.title.y = element_text(size=15,color="DarkBlue"),
    plot.title = element_text(size=20,color="DarkGreen"),
    plot.background = element_rect(fill="LightCyan",color="Maroon")
  ) +
  xlab("Budget Millions ($)")

j + geom_point()

```
  #### Result
  ![Scatter plot showing Audience behaviour with the Budget of the Film](https://github.com/kawal2266/R-for-beginners/blob/master/Plotted%20Graphs/aud_budget.png)
  
  #### Conclusion

  > Audience's Love for the Movie is independent of the Movie's Budget. You need a good script not good set :stuck_out_tongue_winking_eye: 
  > Bingo!


### 4.  Box-Plot - AudienceRating v/s Genre

```R

l <- ggplot(data = movies , aes(x=Genre,y=AudienceRatings,colour=Genre))

m <- l + geom_jitter() + geom_boxplot(size=1.2,alpha=0.70)

m + ggtitle("AudienceRating v/s Genre") + theme(
          axis.title.x = element_text(size=20,color = "Blue"),
          axis.title.y = element_text(size=20,color = "DarkGreen"),
          axis.text.x = element_text(size = 12 , color ="Black"),
          axis.text.y = element_text(size = 10 , color = "Black"),
          plot.background = element_rect(fill="LightCyan",color="Black"),
          plot.title = element_text(size = 25 , color="DarkBlue")
) + ylab("Audience Rating") 

```

  #### Result
  ![Box-Plot to show AudienceRating v/s Genre](https://github.com/kawal2266/R-for-beginners/blob/master/Plotted%20Graphs/aud_genre_boxplot.png) 

  #### Conclusion
  > Median of Thriller, Drama and Romance is high.The Thriller's box is narrow , this shows the deviation in Thriller's liking is least. AudienceRating is likely 
  > to fall between 60 to 75. And Audience loves Drama , as the Maximum value for drama is close to 80 (highest of all)

  #### Let's see what box-plot is ...
  ![What is box-plot](https://github.com/kawal2266/R-for-beginners/blob/master/Plotted%20Graphs/boxplot_explanation.png)

### 5. Histogram - Movie Budget Distribution (Statistical Transformation)

```R

l <- ggplot(data=movies,aes(x=BudgetMillion,fill=Genre))

l + geom_histogram(binwidth = 10,color="Black") +
   ggtitle("Movies Budget distribution") +
  theme(
    axis.title.x = element_text(size=15,color="DarkBlue"),
    axis.title.y = element_text(size=15,color="DarkBlue"),
    axis.text.x = element_text(size=10),
    axis.text.y = element_text(size=10),
    plot.title = element_text(size=20,color="DarkGreen"),
    plot.background = element_rect(fill="LightCyan",color="Maroon"),
    legend.title = element_text(size=20),
    legend.text = element_text(size=15),
    legend.position = c(1,1),
    legend.justification = c(1,1)
)

```

  #### Result
  ![Beautiful Histogram](https://github.com/kawal2266/R-for-beginners/blob/master/Plotted%20Graphs/budget_distribution.png)

  #### Conclusion
  > It's not easy to visualize for a specific genre here!
  > Let's try to have this graph of _Movie Budget Distribution_  for each Genre.
  > This can be done using facets.

### 6. Movie Budget Distribution for each Genre(Using Facets)

```R

l <- ggplot(data=movies,aes(x=BudgetMillion,fill=Genre))

l + geom_histogram(binwidth = 10,color="Black") +
   ggtitle("Movies Budget distribution") +
  theme(
    axis.title.x = element_text(size=15,color="DarkBlue"),
    axis.title.y = element_text(size=15,color="DarkBlue"),
    axis.text.x = element_text(size=10),
    axis.text.y = element_text(size=10),
    plot.title = element_text(size=20,color="DarkGreen"),
    plot.background = element_rect(fill="LightCyan",color="Maroon")
) +
facet_grid(Genre~.)
  
```

 #### Result
  ![Histogram with facets](https://github.com/kawal2266/R-for-beginners/blob/master/Plotted%20Graphs/buget_genre.png)

  #### Conclusion
  > Action Genre plot has the longest tail implying that the high budget movies are made in Action.
  > And Comedy Genre has high number of movies below buget 50 million dollars.

### 7. Audience-Rating and Critic-Rating distribution Comparsion

 * #### Audience-Rating Distribution

    ```R
    i <- ggplot(data=movies , aes(x=AudienceRatings)) + 
    ggtitle("Audience-Rating Distribution") +
    theme(
      axis.text.x = element_text(size=10,color="Black"),
      axis.text.y = element_text(size=10,color="Black"),
      axis.title.x = element_text(size=15,color="DarkBlue"),
      axis.title.y = element_text(size=15,color="DarkBlue"),
      plot.title = element_text(size=20,color="Red"),
      plot.background = element_rect(fill="LightCyan",color="Maroon")
      ) +
      xlab("Audience Rating")

      i + geom_histogram(binwidth=10,fill="White",color="Blue")
    ```
    #### Result
    ![Audience rating Distribution](https://github.com/kawal2266/R-for-beginners/blob/master/Plotted%20Graphs/audience.png)


 * #### Critic-Rating Distribution

    ```R
    i <- ggplot(data=movies , aes(x=CriticRatings)) + 
    ggtitle("Critic-Rating Distribution") +
    theme(
     axis.text.x = element_text(size=10,color="Black"),
     axis.text.y = element_text(size=10,color="Black"),
     axis.title.x = element_text(size=15,color="DarkBlue"),
     axis.title.y = element_text(size=15,color="DarkBlue"),
     plot.title = element_text(size=20,color="Red"),
     plot.background = element_rect(fill="LightCyan",color="Maroon")
    ) +
    xlab("Critic Rating")

    i + geom_histogram(binwidth=10,fill="White",color="Blue")

    ```
    #### Result
    ![Critic rating Distribution](https://github.com/kawal2266/R-for-beginners/blob/master/Plotted%20Graphs/critic.png)

    #### Conclusion
    > Critic-Rating is uniformly distributed but Audience-Rating is not.
    > Audience-Rating is biased.

 ### 8. Audience v/s CriticRating (for Genre and year)

    ```R
    k <- ggplot(data=movies,aes(x=CriticRatings,y=AudienceRatings,color=Genre))

    k + geom_point(aes(size=BudgetMillion),alpha=0.75) + ggtitle("Audience v/s Critic") +
    geom_smooth(fill=NA)+
    facet_grid(Genre~Year) +
    coord_cartesian(ylim=c(0,100)) +
    theme(
     axis.title.x = element_text(size=15,color="DarkBlue"),
     axis.title.y = element_text(size=15,color="DarkBlue"),
     plot.title = element_text(size=20,color="DarkGreen"),
     plot.background = element_rect(fill="LightCyan",color="Maroon")
    )

    ```
  #### Result
  ![Audience v/s Critic rating](https://github.com/kawal2266/R-for-beginners/blob/master/Plotted%20Graphs/aud_critic_year_gen.png)


















