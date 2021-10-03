
# Predicting IMDB Rating on Movies

Connie Xiao

**A Linear Regression Project**

### Abstract
---
The goal of this project is to build a regression model that will determine how well a movie is perceived by the public via IMDB ratings. Clients, such as film production companies, can benefit from this model by being able to predict which movie will have a high IMDB rating. This gives them the ability to gauge how viewers enjoyed their production and to know what features to include in their productions. In order to model the regression, I webscraped data off of IMDB's website. After analyzing the data, we can determine the best key features that would maximize IMDB ratings.

### Data
---
The dataset was gathered from IMDB.com with 10 features in total, 6 numerical and 4 categorical. I was able to receive 3000 data points of movies that were ranked by number of votes. Numerical features include: Metascore, Release Year, Gross Earnings Categorical features include: Genres, MPAA, Director
To predict IMDB ratings,the relationships between variables that may affect the rating (features) should be explored. There are different types of features, categorical and numerical. Start by exploring the correlations between the predictive value and features. Observe if there are any numerical features that collide with each other. To deal with categorical features, we must use Pandas to get dummy variables since it is not possible to compute text-based values into a regression.

### Algorithm
---
#### Data Collection/Cleaning
To gather data, webscrapping was used on IMDB.com with BeautifulSoup. A for loop was created to parse through each page and to extract a selection of features. Features that was able to extracted includes:

- Title
- IMDB Rating
- Number of votes
- Metascore
- MPAA (Content Rating)
- Gross Earnings
- Directors
- Stars
- Genre
- Runtime
- Release Year

I noticed how there was about 200 null values in Gross Earnings and concluded that it was best to drop those rows. Next, it was to make sure there are duplicate entries of the same movie which was about 50 movies. There were couple of null Metascore values as well. Instead of dropping those rows, it was filled in with the dataset's mean Metascore.

#### Feature Engineering
A pairplot and a heatmap was made to visualize the correlations between the numerical features and our target value, IMDB Rating. Metascore and IMDB Rating seemed to have a strong positive correlation, it would be wise to include Metascore as a feature. Votes and Runtime had a positive correlation but not as strong as Metascore, and Release Year had a correlation close to 0.

To determine any severe cases of multicollinearity, the Variance Inflation Factor was used. In this case, Votes and Domestic Gross Earning had fairly low VIF around 2. However Runtime and Release Year had fairly high VIF of 35 and 38. Release Year was removed since it was higher and Runtime and Metascore remained with a VIF around 12.

For the first approach on feature engineering, all the numeric features were included: Runtime, Metascore, Gross Earning and Votes except Release Year since it showed high multicollinearity. The R² score result was 0.616. This was a surprising result.

Next is to add more features. Since Release Year was not incoporated into the engineering, perhaps finding how long since its release could give us a better gauge on the relationship with ratings. It increased the R² score to 0.616.

To face the categorical features, dummy variables had to be extracted. This was done on genres, directors and content rating. After incoporating dummy categories, the R² score was 0.674. So far the engineered features have increase the R² score by 0.06.

After adding the desired features, its time to train and validate the model. Linear and Polynomial Regression was done first. The data set was split up into training and testing sets each with it's desired features and target value. The Polynomial Regression was measured to a degree of 2. R² score for Linear was 0.69 on training and 0.598 on validation. R² score for Polynomial was 0.82 on training and 0.39 on validation. This is a clear overfitting of our model on both regressions.

Next, a Linear vs Ridge Regression was compare using cross validation. Their R² scores were similar: 0.667 with a standard deviation of 0.018.

#### Testing
Given that Ridge Regression and Linear Regression gave the best results, it's time to test them. R² test score for Ridge was 0.587 and R² test score for Linear was 0.598. Although Linear Regression did a better job at fitting, it is clear that the model is overfitting. All 5 validation scares were within similar range and did not raise any concerns.

Finally, its time to put the testing set to the challenge. After finding the optimal alpha for Ridge Regression R² score for the testing set came out to 0.609 with a mean absolute error of 0.384.

Features to include for a good IMDB Rating
To find out the most important features that may contribute to a good IMDB Rating, it is important to look at each feature's coefficient. The biggest contributing factor was how long ago the movie was released. This was a big surprise to for me. Next was Metascore, which made sense since Metascore is a rating system as well. As for categorical features, having content rating of 'Approved' may help, as well as the genres Biography, Family, Drama, Comedy, Thriller and any movies by Steven Spielberg.

### Tools
---
- BeautifulSoup
- Web scraping
- Numpy and Pandas
- Data manipulation
- Seaborn, Matplotlib
- Visuals
- Scikit-learn: StandardScaler, Ridge, Lasso, StandardScaler & Cross Validation
