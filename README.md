<img src=vecteezy_netflix-logo-vector-netflix-icon-free-vector_20336460.jpg alt="Example Image" width="500">

# Netflix-Movie-Data-Analysis-Python-Project
# Project Overview
This project focuses on analyzing Netflix's movie and TV show dataset to extract meaningful insights. It involves Exploratory Data Analysis (EDA) to uncover trends, patterns, and relationships in the data
.
# Key Objectives

# 1️. Handling Null Values

Identify Null values  in the dataset. Show the Null values using heatmap plot.

# 2️. Removing Duplicates
Detect and remove duplicate rows to maintain data integrity.

# 3️. Fixing Data Inconsistencies

change column names (e.g.type to category).
Correct inconsistent formats in numeric, and categorical data.

# 4️. Handling Incorrect Data Types
Convert columns to appropriate data types (e.g., date added to datetime).

# 5️. Parsing and Splitting Data

Extract meaningful information (e.g., splitting duration into Minutes and Unit).

# 6️. Removing Unnecessary Data

Drop irrelevant or redundant columns that don’t contribute to analysis.

# Feature Engineering
Create new column  release_date for datetime dtype. 
Create new column  year extract from  the release_date  Coulumn. 
Create new column  Minutes and Unit  Using duration   Column.

# Technologies Used
Python (python, or Excel) – for data extraction, transformation, and analysis.
Excel / Power BI / Tableau (Optional) – for visualization and dashboard reporting.

## About Data

This project's data was obtained from the  website kaggle  data extract for creating insights 
The data contains 12 columns and 8807 rows:
| Column            | Description                                   | Data Type        |
|-------------------|-----------------------------------------------|------------------|
| show_id           | Gives Show Unique id                          | object           |
| category          | Gives the category of shows                   | object           |
| title             | Gives the name of shows                       | object           |
| director          | Gives director name of shows                  | object           |
| cast              | Gives cast name of shows                      | object           |
| country	        | Gives origin country name of shows            | object           |
| date_added        | Gives release date of shows                   | object           |
| release_year      | Gives the release year of shows               | int64                |
| rating            | Gives the rating of shows                     | object           |
| duration          | Gives the duration of shows                   | object           |
| listed_in         | Gives type of shows                           | object           |
| description       | Gives description of show                     | object           |
| release_date      | Gives the release date of shows               | datetime64       |
| Year              | Gives the release year of shows               | float64          |
| Minutes           | Gives the show duration in minutes            | float64          |
| Unit              | Gives the unit of duration                    | object           |



# Conclusion and Recommendations:
This analysis provides a comprehensive overview of Netflix’s content distribution and trends. Future work can focus on sentiment analysis of movie reviews, recommendation systems, and deeper insights into user preferences based on viewing patterns.

## Questions to Answer

# Q.1 Is there null values present in any column? show with heatmap
Ans: sns.heatmap(df.isnull()) 

# Q.2 For 'House of Cards',What is the show id and who is the Director of this show?
Ans: df[df['title'].str.contains('House of Cards')]

# Q.3 . In which year highest no of tv Shows and movies where released? Show with Bar Graph
Ans: df['release_date'] = pd.to_datetime(df['date_added'], format='mixed', errors='coerce')
     df['release_date'].dt.year.value_counts()

# Q.4. How many Movies & TV Shows are in the dataset? Show with Bar Graph
Ans: df = df.rename(columns={'type':'category'})
     df.groupby('category').category.count()
     sns.countplot(df['category'])

# Q.5 Show all the movies that where released in year 2000
Ans: df['year']= df['release_date'].dt.year
     df_filtered = df.query("category == 'Movie' and year == 2000")
  
 # Q.6 Show only the titles of all Movie that were released in india only 
 Ans: df_filtered = df.query("category == 'Movie' and country == 'India'")['title']

# Q.7 Show top 10 Directors, who have the highest number of Tv Shows and Movie  to netflix
 Ans: df['director'].value_counts().head(10)

# Q.8 Show all the records, where "category is Movie and type is comedies" or "Country is United Kingdom"
Ans: df_filtered = df.query("(category == 'Movie' and  listed_in == 'Comedies') or country == 'United Kingdom'")

# Q.9 In how many Movies/ Tv shows, Tom Cruise cast?
Ans: df_filtered = df[df['cast'].str.contains('Tom Cruise

# Q.10 What are the different Rating defined by Netflix?
Ans: df.rating.nunique()
     df.rating.unique()

# Q.10 1. How many movies got the 'TV-14' rating in canada
Ans:df[(df['category'] == 'Movie') & (df['rating'] == 'TV-14') & (df['country'] == 'Canada')].shape


# Q.10.2.How many 'TV Show got the 'R' rating, after year 2018
Ans: df[(df['category'] == 'TV Show') & (df['rating'] == 'R') & (df['year'] > 2018)]

# Q.11 What is the Maximum duration of a Movie/TV Show on netflix?
Ans: df[['Minutes','Unit']]= df['duration'].str.split(' ', expand= True)
     df['Minutes'].max()

# Q.12 Which individual country has the highest No. of Tv Shows
Ans: df_tvshows = df[df['category'] == 'TV Show']
     df_tvshows.country.value_counts().head(1)     

# Q.13 How can we sort the dataset by year?¶
Ans: df.sort_values(by='year', ascending= False).head(1)

# Q.14 Category is 'Movie' and listed_in in 'Dramas' Or category is 'TV Shows' and listed_in in 'Kids' 'Tv'
Ans: df_filtered = pd.concat([ df[(df['category'] == 'Movie') & (df['listed_in'] == 'Dramas')],
df[(df['category'] == 'TV Show') & (df['listed_in'] == "Kids' TV")]])
