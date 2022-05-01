# Project 3 - Classifying posts from two subreddits, r/WeddingPlanning and r/Divorce

## Problem Statement

We have been contracted by a divorce lawyer who is trying to improve targeted advertisement of her services. She usually uses keywords such as divorce, marriage and family to target her advertisements, but she has been receiving feedback that her ads are also being shown to engaged couples and newlyweds. She would like us to develop a model for classifying wedding planning vs divorce posts that she could bring to advertisers to potentially incorporate in her next advertisement campaign. Her goal is to try to advertise to as many potential divorce clients as possible but avoid as many wedding planners so that she doesn't turn off potential future clients and waste precious avertising dollars.

## Source
The project collects a total of 8,000 Reddit posts from r/WeddingPlanning and r/Divorce using [Pushshift's API](https://github.com/pushshift/api). 

---
## Summary of Analysis
The data was split into train and test sets at a 75% split. The train dataset was used to generate various classification models using the Reddit post text and title text. The test dataset was used to test the model accuracy and other metrics on unseen data.

Code Structure:
1. Data Collection
    - Function to pull posts using Pushshift's API
    - Exploratory data analysis to identify outliers, remove duplicates, and verify the data has potential for solving the problem
2. NLP Pipeline Model
    - Train-test split
    - Column transformer to count vectorize words/phrases in posts and titles
    - Pipelines using column transformer:
        - Logistic Regression
        - K Nearest Neighbors
        - Decision Tree Classifier
        - Random Forest Classifier
        - Extra Trees Classifier
        - Multinomial Naive Bayes
        - Ada Boost Classifier
    - Grid searching for count vectorizer and model hyperparameters
    - Voting classifier combining the models above
    - Selection of the production model
3. Evaluation Production Model
    - Comparison of baseline and production model accuracy and recall score
    - Inference of production model coefficients and feature importances
    - Review of divorce post misclassifications
    - Conclusion and recommendations
    
---
    
## Directory Structure

project-3
- code
    - 01_Data_Collection.ipynb
    - 02_NLP_Pipeline_Model.ipynb
    - 03_Evaluation_Production_Model.ipynb
- datasets
    - combined_cleaned.csv
    - combined.csv
    - divorce.csv
    - misclassifications.csv
    - wedding.csv
- images
    - various images used in presentation
- presentation.pdf
- README.md

---

## Conclusions and Recommendations

The production model is ready to be deployed as a model to separate out wedding planning posts from divorce posts.

The production model is works on r/WeddingPlanning and r/Divorce posts with 97.4% accuracy. This ensures the lawyer will not waste precious advertising dollars on wedding planners and potentially annoy the wedding planners, who might eventually become clients in a few years.

Additionally, the model correctly classifies divorce posts 99% of the time, so the lawyer is advertising to 99% of the potential clients, only missing 1%.

The next steps for the lawyer would be to share this technical report with her advertising coordinators/partners so they can implement this modeling pipeline to filter out wedding planning related posts. The advertising partners may wish to collect more data to further improve the model and focus in on key coefficients that seem to be overly low/high even though the word appears frequently in both divorce and wedding planning posts.