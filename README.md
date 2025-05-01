## Project Goal
This project is to analyze and predict the prices of Airbnb in New York City. The goal is to uncover patterns that inform pricing decisions for Airbnb stakeholders - hosts, guests, and the platform.

## Introduction
Airbnb offers travelers different experiences while creating opportunities for homeowners to earn money from their spaces. However, pricing is a key challenge for both hosts and guests.  This project focuses on answering a critical question: What factors influence Airbnb pricing, and how can we predict prices accurately? We will build machine-learning models to predict Airbnb prices based on features like locations, reviews, room types, and availability. 

## Dataset
This is from Kaggle.
* [new_york_listings_2024.csv](https://www.kaggle.com/datasets/vrindakallu/new-york-dataset) consists of 20,758 Airbnb listings in New York City in 2024. It contains 22 numerical and categorical features, offering insights into various aspects of rental properties.
* [neighborhood_score.csv](https://www.walkscore.com/professional/research.php) includes 5 columns: walk_score, bike_score, transit_score, and population, which represent neighborhood-level attributes.

## Exploratory Data Analysis (EDA)
### 1. Price Distribution
* Range: Prices range from $10 to $90,000, with the majority of listings priced between $50 and $500.
* Distribution: The price distribution is heavily skewed, reflecting the diversity in room types and neighborhoods.
### 2. Room Type Breakdown
* Entire homes/apartments makeup 55.6% of listings.
* Private rooms account for 42.4%.
* Shared and hotel rooms constitute less than 2%, indicating limited demand for communal spaces.
* Price differs from different room type
### 3. Neighborhood Analysis (Strongly correlate with price)
* Manhattan: Has the highest average price of $227.85, driven by luxury apartments.
* Brooklyn: Offers more affordable options, with an average price of $187.03.
* Queens: Features budget-friendly listings, with an average price of $126.49.
### 4. Correlation Heatmap
* Price shows a weak relationship with most other features.
* Price shows negative relationship with minimum night
* Price is moderate correlated with the scores, number of bedrooms, number of beds, and number of baths
### 5. Availability and Price
* Listings available for 365 days tend to have lower prices, suggesting they cater to budget-conscious renters.

## Data Cleaning and Feature Engineering
### 1. New Features
* `review_recency`: The number of days since the last review, calculated as the difference between the current date and the `last_review` date. We created this feature to integrate the recency of the last review.
### 2. Filling Missing Values
* `baths`: Missing or unspecified values ('Not specific') were replaced with 0.
* `ratings`: Missing or categorical placeholders like 'No rating' or 'New' were replaced with 0.
* Neighborhood Scores: Missing values for `walk_score`, `bike_score`, `transit_score`, and `population` were filled using the values of the nearest neighborhood, identified based on the closest latitude and longitude.
### 3. Outliers
* We find the numerical features `price`, `bedrooms` and `beds` are the ones may have most of outliers, so we were capped using the interquartile range (IQR) method:
* Values below Q1−IQR were set to Q1−IQR
* Values above Q3+IQR were set to Q3+IQR
### 4. Encoding
* Categorical variables were label-encoded to prepare them for predictive modeling.

## Key Findings
The analysis of Airbnb listings in New York City revealed several critical insights into pricing dynamics. Location significantly impacts listing prices, with Manhattan and Brooklyn commanding the highest average prices due to their premium appeal and central accessibility. Conversely, more affordable options are concentrated in Staten Island and the Bronx, catering to budget-conscious renters. This variation in pricing highlights how location remains a key determinant of rental value in the city.

Room type also plays a substantial role in pricing differences. Entire homes/apartments and private rooms dominate the market, reflecting their popularity among renters, while hotel rooms, despite being less common, are the most expensive on average. The variation in room types demonstrates how property offerings cater to diverse renter preferences, with larger or more private accommodations attracting higher rates.

Correlations among numerical features provide additional insights into price determinants. Property size, represented by the number of beds, bedrooms, and baths, shows a strong positive relationship with price, indicating that larger properties command significantly higher rates. Location-based amenities, such as walk, bike, and transit scores, moderately influence pricing, as higher scores correlate with higher prices. These findings emphasize the importance of accessibility and convenience in driving rental values. However, some outliers exist, where prices deviate significantly from the expected trends, underscoring the variability in the market.
