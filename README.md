# Analyzing-Google-Play-Store-App-Ratings-and-Trends
Analyze Google Play Store data to understand factors influencing app popularity and user satisfaction.

# Project Description:
This project aims to delve into the Google Play Store dataset, exploring key metrics, identifying patterns, and uncovering valuable insights related to app ratings, categories, reviews, and other relevant factors. By conducting in-depth analysis, we seek to understand the factors influencing app popularity and user satisfaction, providing valuable insights for developers and marketers.

# Exploratory Data Analysis

### 1. Exploratory Data Analysis

Average, Minimum, Maximum, and Standard Deviation of Ratings: Calculates these statistics to understand the overall distribution of app ratings.
Category Distribution: Counts the number of apps in each category to identify the most popular ones.
Top-Rated Apps: Lists the 5 apps with the highest ratings.

### 2. Correlation Analysis

Correlation between Rating and Size: Examines the relationship between app ratings and their size to see if there's a correlation.

### 3. Additional Queries

- Top 5 Apps with Highest Ratings: Lists the top 5 apps based on their ratings.
- App Count by Category: Counts the number of apps in each category and orders them by count.
- App Ranking within Category: Ranks apps within their respective categories based on ratings.
- Apps with Above-Average Ratings: Identifies apps that have ratings higher than the average rating for their category.
- Average Rating of Apps with Many Reviews: Calculates the average rating for apps with more than 1,000 reviews.
- App Count by Type: Counts the number of apps that are free or paid.
- Overall, these queries provide valuable insights into the Google Play Store dataset, such as the distribution of ratings, popular categories, and the relationship between app -attributes and ratings.

## Schema

```sql
CREATE TABLE google_play_store (
    app_name TEXT,
    category TEXT,
    rating FLOAT,
    reviews INTEGER,
    size FLOAT,
    installs INTEGER,
    type TEXT,
    price FLOAT,
    content_rating TEXT,
    genres TEXT,
    last_updated TEXT,
    current_version TEXT,
    android_version TEXT
);
```

## Analysis and Findings

```sql
SELECT AVG(Rating), MIN(Rating), MAX(Rating), STDDEV(Rating)
FROM google_play_store;

SELECT Category, COUNT(*)
FROM google_play_store
GROUP BY Category;

SELECT App_Name, Rating
FROM google_play_store
ORDER BY Rating DESC
LIMIT 5;
```
```sql
-- Correlation Analysis

SELECT CORR(Rating, Size)
FROM google_play_store;
```


## Q.1.Find the Top 5 Apps with the Highest Ratings
```sql
SELECT
  App_Name,
  Rating
FROM
  google_play_store
ORDER BY
  Rating DESC
LIMIT 5;
```

## Q.2. How many apps are in each category, ordered from most to least?
```sql
SELECT Category, COUNT(*) AS App_Count
FROM google_play_store
GROUP BY Category
ORDER BY App_Count DESC;
```

## Q.3. What is the rank of each app within its category based on rating?
```sql
SELECT App_Name, Category, Rating,
       RANK() OVER (PARTITION BY Category ORDER BY Rating DESC) AS Rank
FROM google_play_store;
```
## Q.4. Which apps have ratings above the average rating for their respective categories?
```sql
SELECT App_Name, Rating, Category
FROM google_play_store
WHERE Rating > (
  SELECT AVG(Rating)
  FROM google_play_store AS avg_table
  WHERE google_play_store.Category = avg_table.Category
);
```

## Q.5. Average Rating of Apps with More Than 1,000 Reviews
```sql
SELECT
  AVG(Rating) AS Average_Rating
FROM
  google_play_store
WHERE
  Reviews > 1000;
```

## Q.6.Count the Number of Apps by Type (Free vs Paid)
```sql
SELECT
  Type,
  COUNT(*) AS App_Count
FROM
  google_play_store
GROUP BY
  Type
ORDER BY
  Type;
```

### Author : SRIDHAR

I am a self-taught data analyst currently honing my skills through YouTube tutorials and a Coursera course. In this project, I utilized data analysis techniques along with SQL, Python, and ChatGPT to enhance my understanding and capabilities in the field. I am also in my final year of pursuing a BCA degree through correspondence, which I expect to complete soon. This experience has significantly improved my skills, and I am actively seeking internship opportunities to further develop my expertise and gain practical experience in data analysis.
  
### Tools and Technologies:

- Programming Language: Python
- Database: PostgreSQL
- Pandas,git,chat gpt,MS excel

### Recommendations:

Target popular categories
Prioritize user feedback
Enhance app performance
Consider in-app purchases carefully
