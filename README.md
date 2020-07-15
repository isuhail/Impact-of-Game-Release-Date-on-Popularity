# Impact-of-Game-Release-Date-on-Popularity

## Project Overview

As a leading publisher of video games, the client is interested in distributing their newest developed games through an online game distributor, Steam. Observing that many games released during the winter also saw a larger number of buyers, the client is eager to find out if there exists a causal effect between the winter release time and the popularity of the game in terms of number of owners to make strategic decisions on the release time of their new game. However, to make such a causal claim, the team is faced with many challenges with respect to confounding factors that could bias their conclusion of a relationship existing or not. Variables, like category and price, both influence the game release date and popularity. In order to address such threats, the team applied propensity score matching to eliminate these effects and to capture the real effect of the winter release on the number of owners. Through careful analysis,the team found that there is no significant effect of releasing games in the winter on the number of buyers. The team also discusses limitations of their analysis and future steps that can be taken to enhance their exploration and understanding of a good time to release games.

## Data 

Using data gathered from the Steam Store and SteamSpy APIs, this dataset provides information about various aspects of games on the store, such as its genre and the estimated number of owners.

Gathered around May 2019, it contains most games on the store released prior to that date. Unreleased titles were removed as well as many non-games like software, though some may have slipped through.

More details about the dataset can be found here:

https://www.kaggle.com/nikdavis/steam-store-games

## Approach

![Methodology](https://github.com/isuhail/Impact-of-Game-Release-Date-on-Popularity/blob/master/Methodology.png?raw=true)

Ideally, to understand the effect of release date on popularity, an experiment should have been  conducted such that similar games are released randomly on different dates. Since we are dealing with observational data, we need to find pairs of treated units and control units that are as similar as possible on  price, game quality (based on ratings and average play time), genre, and category such that the choice of the release date for the game can be considered as good as random and not getting affected by these factors. Therefore the matching technique has been used. After matching, we conduct a regression to detect the causal relationship purely between game popularity and treatment. 

### Propensity Score Matching:

We used a technique called propensity score matching. Here we calculate the probability of a game releasing in winter. We use all the factors that could affect the release of a game  to calculate this probability.  Pairs of observation in treatment and control group with similar probability are matched. In such a scenario, we can say that the games are released in winter by a random chance. 

Assumption:

By conducting propensity score matching, we make 2 major assumptions:
1. Conditional Independence Assumption: 
This assumption is also known as selection on observables, and it requires our chosen covariates to include all variables relevant to the probability of receiving treatment. After controlling these variables, the potential popularity for the game is independent of treatment status.
The conditional independence assumption cannot be directly tested, but we have certain level of confidence in arguing that all relevant variables have been included because we believe the logical unobserved confounders, such as developer reputation, financial pressures are highly correlated with the covariates in our model, which are price, rating, in-game achievements, game type.

2. Common support Assumption: 
For each game with a combination of characteristics, there is a positive probability to be treated( released in winter) as well as a positive probability to be untreated(released during the rest of the year). This assumption ensures that there is sufficient overlap in the characteristics of treated and untreated units to find adequate matches.

### Linear Regeression:

After matching the data we run a regression to measure the change in popularity due to the treatment which is releasing the game during winters

## Results and Conclusion

Model results show us that releasing the game in winter months will increase the sales of the game by 0.19. However, this result is not strongly supported. Value of standard error is higher than the beta coefficient of treatment which is not ideal. Moreover, the p-value is 0.407 which means that we are observing a relationship between the treatment and popularity of games by chance. R squared value is very low as well which means that the model does not explain the data very well.
Increasing the sample size by collecting more data should help us get more significant results here. The results we get right now are not very representative of the data. 


## Final Recommendation:
From the regression result, no significant treatment effect is observed after matching. Thus, releasing games during winter months (October, November, and December) will not have a causal effect on the success of the game in terms of number of owners. However, due to sample size limit, our results are not very significant. Collecting more data and then running the test again will help us get more concrete results.


