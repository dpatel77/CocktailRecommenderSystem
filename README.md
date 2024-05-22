# Cocktail Recommender System
**Using Real & Synthetic Data for Recommendations Evaluation**

**Using Machine Learning to Suggest Cocktails**

**Dharti Seagraves**

**Date: May 22, 2024**

---

## Problem Statement
- **Objective:** Create a cocktail recommender system using cocktail features and user ratings data
- **Importance:**
  - Personalized recommendations can enhance user experience and satisfaction in cocktail selection
  - Helps users discover new cocktails tailored to their tastes
  - Can help generate revenue for bars and restaurants
- **Motivation:** Improve customer engagement and satisfaction in the beverage industry

---

## Dataset
- **Cocktail Data Source:** Web scraped from CocktailViz
  - 48 cocktails, 22 features
  - Details on ingredients, alcohol content, and flavor profiles
- **User Ratings Data Source:** Collected via a Google Form survey
  - Included user preferences and ratings on various cocktails
- **Dataset Size:**
  - Real Data: 115 records (actual user ratings)
  - Synthetic Data: 10,000 records (generated to compare with a larger dataset)

---

## Assumptions and Hypotheses
- **Assumptions:**
  - User preferences are consistent over time
  - Survey bias does not exist
  - Synthetic data is a reliable approximation of real user behavior
- **Hypotheses:**
  - Feature importance aligns with user preferences
  - Synthetic data will not replicate real user data because it lacks real-world patterns (used primarily for the quantity of records)

---

## Exploratory Data Analysis
- **Correlation Matrix:**
  - No multi-collinearity
  - 117 features after Feature Scaling
- **Distribution Analysis:**
  - Even distribution of liquors and alcohol content
- **3D Distribution of Users, Cocktails, and Ratings:**
  - Synthetically generated user ratings:
    - Train/test split: 7500/2500
    - Unique Users: 2k

---

## Feature Engineering & Transformations
- **Feature Engineering:** None conducted
- **Transformations:**
  - Normalization, encoding, and scaling techniques applied to improve model performance
  - Standard Scaling numerical values:
    - ['Alcohol', 'Base Wine Amount', 'Salty', 'Savory', 'Sour', 'Bitter', 'Sweet', 'Spicy']
  - One-hot encoding categorical values:
    - ['Category', 'Making', 'Base Wine', 'Liquor', 'Liquor Amount', 'Juice', 'Juice Amount', 'Spice', 'Spice Amount', 'Soda', 'Soda Amount', 'Others', 'Taste', 'Type of Glass']
- **Feature Importance:**
  - Sweet: 0.000569
  - Juice_Pineapple: 0.000374
  - Alcohol: 0.000354
  - Liquor_Green Mint: 0.000147
  - Base Wine_Rum: 0.000140

---

## Model Development
- **Approaches:**
  - Item-based Collaborative Filtering: Recommends items similar to those the user liked
  - User-based Collaborative Filtering: Recommends items liked by similar users
  - Content-based Filtering: Recommends items similar to those the user has liked based on features
  - SVD-based Collaborative Filtering: Uses matrix factorization to predict user preferences
- **Overfitting and Underfitting Checks:**
  - Learning Curves: Analyzed to determine if models are learning effectively

---

## User Profiles (Item-Based)
- **User 2's Top-Rated Cocktails:**
  - Tom Collins (5)
  - Gin & Tonic (4)
  - Mojito (4)
  - Black Russian (4)
  - Manhattan (3)
  - Screwdriver (3)
  - Cosmopolitan (1)
  - Bloody Mary (1)
  - Tequila Martini (1)
- **Recommendations:**
  - Blue Hawaii: Similar to Tom Collins
  - Vodka & Tonic: Similar to Gin & Tonic
  - Martini
- **Similarity Insights:**
  - User 38 rated both Tom Collins and Blue Hawaii highly

---

## User Profiles (User-Based)
- **User 2's Top-Rated Cocktails:**
  - Tom Collins (5)
  - Gin & Tonic (4)
  - Mojito (4)
  - Black Russian (4)
  - Manhattan (3)
  - Screwdriver (3)
  - Cosmopolitan (1)
  - Bloody Mary (1)
  - Tequila Martini (1)
- **User 38's Top-Rated Cocktails:**
  - Gin & Tonic (5)
  - Moscow Mule (5)
  - Bloody Mary (5)
  - Margarita (5)
  - Blue Hawaii (4)
  - Tom Collins (4)
  - Long Island Ice Tea (4)
  - Manhattan (4)
  - Tequila Sunset (3)
  - Vodka & Tonic (3)
  - Screwdriver (1)
- **Recommendations:**
  - Martini
  - Moscow Mule
  - Long Island Ice Tea
- **Similarity Insights:**
  - User 2 is most similar to User 38 based on the similarity matrix

---

## User Profiles (Content-Based)
- **User 2's Top-Rated Cocktails:**
  - Tom Collins (5)
  - Gin & Tonic (4)
  - Mojito (4)
  - Black Russian (4)
  - Manhattan (3)
  - Screwdriver (3)
  - Cosmopolitan (1)
  - Bloody Mary (1)
  - Tequila Martini (1)
- **Recommendations:**
  - Horse’s Neck
  - Moscow Mule
  - Vodka & Tonic
- **Similarity Insights:**
  - Based on Category, Making, and Taste similarities

---

## User Profiles (SVD)
- **User 2's Top-Rated Cocktails:**
  - Tom Collins (5)
  - Gin & Tonic (4)
  - Mojito (4)
  - Black Russian (4)
  - Manhattan (3)
  - Screwdriver (3)
  - Cosmopolitan (1)
  - Bloody Mary (1)
  - Tequila Martini (1)
- **Recommendations:**
  - Margarita
  - Old Fashioned
  - Moscow Mule
- **SVD Insights:**
  - Leverages matrix factorization to reveal latent relationships between users and items

---

## Model Evaluation
- **Visualization:**
  - Learning curves for the SVD model on both real and synthetic datasets for 20 epochs
- **Metrics:**
  - Real data - Train RMSE: 1.31 Test RMSE: 1.17
  - Synthetic data - Train RMSE: 0.97 Test RMSE: 0.97
- **Observations:**
  - Real Data: The training RMSE steadily decreases, indicating learning. The testing RMSE remains stable with a slight increase towards the end, indicating potential overfitting.
  - Synthetic Data: The synthetic data starts with similar RMSE values. The test RMSE has a steeper curve, indicating quicker learning and good generalization.

---

## Results & Learnings
- **Summary of RMSE Values:**
  - Item-Based Collaborative Filtering RMSE: 3.86
  - User-Based Collaborative Filtering RMSE: 3.83
  - Content-Based Filtering RMSE: 2.96
  - SVD-Based Collaborative Filtering RMSE: 1.13
- **Conclusion:**
  - The best model for the given real dataset was the SVD model with the lowest RMSE.
  - The SVD model provides the closest recommendations to the user’s actual ratings.
  - Latent factors in SVD influence user preferences for more accurate recommendations.
  - The SVD model is recommended for making cocktail recommendations.

---

## Future Work
- **Increase the Volume of Data:**
  - Collect more real user ratings to improve model accuracy.
  - Aim for at least 1000 real user ratings to better understand user preferences.
- **Reduce User Bias:**
  - Randomly showcase a few cocktails for users to rate versus allowing users to choose.
- **Explore Advanced Algorithms:**
  - Regularization and Hyperparameter Tuning.
  - Neural Collaborative Filtering.
  - Hybrid Models.
- **Incorporate Time-Series Elements:**
  - Track how user preferences change over time.
- **A/B Testing and Continuous Improvement:**
  - Implement A/B testing to evaluate model performance and improve iteratively.
- **Expand Cocktail Selection:**
  - Include a more diverse range of cocktails, including non-alcoholic options.

---

**THANK YOU!**
