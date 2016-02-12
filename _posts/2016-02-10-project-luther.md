---
published: true
---

## Entering Week 4 of Metis
It feels as though it's been in some ways longer, and others shorter, than the three weeks it's actually been since starting Metis. But three weeks is how long it's been. Technically three weeks and one day. The impetus for this blog post is to wrap up thoughts on 'Project Luther' which we finished and gave presentations on on Monday.

## Looking At Weekly Box Office Returns & Movie Reviews
For our second project of the bootcamp, we were tasked with using data scraped from Box Office Mojo to model outcomes of movies. Narrowing it down from there was left up to us, and I decided to look at weekly box office returns along with review data scraped from Metacritic. One thing I was especially curious about going into the project was if better reviewed movies had greater longevity at the box office.

### Part 1: Web Scraping & Data Acquisition
Web scraping was one of the things I was really looking forward to getting better at at Metis, and this project provided ample opportunity to ply those skills. I decided to scrape data from two different sources, Box Office Mojo as well as Metacritic. To do so, I used Python HTML parser BeautifulSoup. I wanted to get as many movies as possible, so I wrote functions that would run through every page in both Box Office Mojo's and Metacritic's list of movies. For BMO, I wanted week-by-week data, so I scraped the each page of their list of movies, then using the movie URLs from that page, I scraped weekly data for each movie on their site. I ended up with 13,890 movies from BMO, and it took almost two hours to scrape it all.

Since I wasn't getting as much detail on movies from Metacritic, I only had to go through their pages of movies. Their site was structured a bit differently, so I had to use a different function to scrape it. I ended up with 7,719 movies from Metacritic. I'm pretty sure the BMO's data is more thorough, although it's also entirely possible that my scraping of each sight wasn't exhaustive. In any case, I felt that I had a pretty robust data set to work with.

### Part 2: Analysis & Conclusions
Having data from two different sources, I needed to combine it into one data set to work with. I used Pandas to structure my data, so it was fairly straightforward to merge. I matched titles of movies from my BMO and Metacritic sets in order to merge. One hurdle I did have to clear was dealing with movies with different sub-titles or punctuation in the titles.

I ran some initial analysis on the merged data, focusing on the effect of Metacritic scores. I quickly found that the majority of movies I was looking at had very small theater counts. Since I was looking at weekly box office returns, this was an issue. Here's a histogram of the distribution of opening week theater counts:
![Opening Week Theater Count]({{site.baseurl}}/_posts/opening_week_thtrs.png)

Due to this, I decided to focus my analysis on movies with wide releases (>600 theaters).

Since I was curious about Metacritic scores, I looked at a correlation table. Here were the top results:
![Screen Shot 2016-02-11 at 4.21.42 PM.png]({{site.baseurl}}/_posts/Screen Shot 2016-02-11 at 4.21.42 PM.png)

So higher metacritic scores are correlated with average gross per theater, more so than total weekly gross. This makes sense to me, because a film's total gross is also dependent on how many theaters it is released in. Seeing this, I decided to focus my analysis on per theater gross.

I ended up coming up with a model that predicts week 2 theater average based on week 1 theater average and metacritic score. I found that week 1 theater average was a strong predictor on its own, but that metacritic score did have a significant effect. Here are the results of my model:

![Screen Shot 2016-02-11 at 4.40.26 PM.png]({{site.baseurl}}/_posts/Screen Shot 2016-02-11 at 4.40.26 PM.png)

Here is a plot showing my fitted model against actual values:![fitted.png]({{site.baseurl}}/_posts/fitted.png)

As you can see, the model does a pretty good job for most movies. The effect of metacritic score is about $30 per theater per point increase in score. That means that for every point the score increases, the theater average goes up by $30. Given ticket prices, that means about 3 more people will see a movie for every metacritic point. So well reviewed movies might not sell out a theater, but they do have a statistically significant effect.

### Part 3: Further Steps

While my findings weren't revolutionary, I learned a lot about how to handle data science projects from end to end, and enjoyed this project. I was ambitious in how much data I was collecting, which I'm glad about because I got a lot better at web scraping. However, I ended up not using most of it, and even lacking some data that I could have used.

One thing that would have been interesting to look at was time data. The Oscars are a significant event in the film industry, and I believe that there is a small boost during Oscar season for films with nominations. Another thing to look at would have been genre, since perhaps critical score is more important for say, Dramas than it is for Action movies. 

Another thing I'd have done differently is to come up with a model to generalize weekly box office returns. I only came up with models to look at one week based on other weeks. This was partially because of the way I structured my data. Knowing what I know now, I would have planned my data acquisition and structure in a way that would have been more ideal for analysis. 

All in all, I thought this was a successful and productive project, and I'm pleased with my results and with what I learned from it. I'll have plenty to take from this and to apply to my next project.
