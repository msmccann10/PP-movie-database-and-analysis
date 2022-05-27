# **Movie Database and Analysis**

**Author:** Michael McCann <br>
**Late Updated:** 21 MAY 2022
___

## Overview
My customer has requested that I recommend strategies for making a successful movie based on data available on IMDB and TMDB. To accomplish this task I extracted data from IMDB and TMDB, transformed/cleaned the data, and loaded it into a MySQL database for EDA, hypothesis testing, and predictive modeling. 

The primary indicator of success for my analysis is revenue which measures the total amount of income generated by the movie. To conduct my analysis I set out to answer the following questions:
1. Does the MPAA rating affect the revenue of a movie? Which ratings perform best/worst?
2. Does genre affect the revenue of a movie? Which genres perform best/worst?
3. Has runtime (in minutes) increased or decreased significantly over the past 20 years?
4. Do longer movies do better than shorter movies? 

## Business Problem 
A fictional customer is the newly appointed head of a production company. They want their first movie as the head of their company to be a major success and want to use data to optimize their movie and increase the likelihood of success. Revenue is the primary indicator of success for this analysis.

## Data
### Data Sources
The data for this project comes from two separate sources. These datasets were extracted, transformed, and loaded into a MySQL database for analysis as part of this project. Our data sources are as follows:
- [IMDB's Publically Available Data](https://datasets.imdbws.com/): IMDB provides basic information and statistics on movies within their database from which we can pull a majority of the information needed for our analysis. 
- [TMDB Movie Data](https://www.themoviedb.org/): Accessed through the [tmdbsimple](https://github.com/celiao/tmdbsimple) API package we were able to augment the data available on IMDB with financial information (budget, revenue) and MPAA rating.

The original dataset has been stored in this repository and can be found [here](https://github.com/msmccann10/PP-movie-database-and-analysis/tree/main/data). The data was subsequently turned into a MySQL database for easier access and analysis.

### Data Dictionary
We used the following features from the IMDB and TMDB databases for our analysis. 

|Feature|Description|Source|Type|
|---|---|---|---|
|primaryTitle|the title used by the filmmakers on promotional materials|IMDB Database|string|
|startYear|represents the release year of a title|IMDB Database|numeric|
|genre_name|the genres associated with the title|IMDB Database|string|
|certification|MPAA rating for the movie (eg: PG-13)|TMDB API|string|
|runtimeMinutes|primary runtime of the title, in minutes|IMDB Database|numeric|
|belongs_to_collection|Represents if a film is part of a series or a stand alone|TMDB API|boolean|
|revenue|ammount of money generated by the film|TMDB API|numeric|
|budget|ammount of money spent producing the film|TMDB API|numeric|
|status|status of the film in the database|TMDB API|string|
|product_company|company or companies responsible for producing the film|TMDB API|string|
|averageRating|weighted average of all the individual user ratings|IMDB Database|numeric|
|numVotes|number of votes the title has received|IMDB Database|numeric|

The following features are referential for our MySQL database but will not appear in our analysis, hypothesis testing, or modeling

|Feature|Description|Type|
|---|---|---|
|tconst|alphanumeric unique identifier of the title|string|
|genre_id|numeric identifier representing film genres|numeric|
|prodco_id|numeric identifier representing production companies|numeric|

Full data dictionaries, including features not used for our analysis, can be found at [IMDB](https://www.imdb.com/interfaces/) and [TMDB's](https://developers.themoviedb.org/3/movies/get-movie-details) respective websites.

<!--- - A full data dictionary for the IMDB datasets can be found [here](https://www.imdb.com/interfaces/)
- A full data dictionary for the TMDB API can be found [here](https://developers.themoviedb.org/3/movies/get-movie-details) --->

### Data Selection
The following choices were made regarding what data to keep or cut for this study:

- Release Year: For our study we limited the entries in our dataset to movies released from 2000 to the present. This timeframe was selected to give us a large enough sample size while also not extending so far into the past as to have different tastes/preferences. 
- Genre: Documentaries were cut from the dataset at the request of our customer. Documentaries often differ from traditional ‘entertainment’ films in terms of budget, revenue, ratings, etc which might have changed the shape of our data and impacted our analysis.
- MPAA Rating: Our customer expressed an interest in movies rated G, PG, PG-13, and R, so movies that were either unrated or rated NC-17 were removed from our dataset. Unrated/NC-17 movies tend to be more elicit or less reputable, things our customer is looking to avoid at this time. 

### Data Validation
Duplicates: Missing Values: Inconsistent Data: Minor changes were made to the MPAA Ratings and Outlet Size columns for consistency. MPAA Ratings: Multiple entries are used to indicate the same value (IE: ?? and ??). Some values included spaces or punctuation which were recoded for consistency.  

### Caveats and Considerations
The dataset documentation does not provide clear guidelines/definitions for the variables within Outlet Size, Outlet LocationType, and Outlet Type (IE: what constitutes a small vs large outlet, what differentiates a supermarket type 1 from a supermarket type 3). These variables are therefore taken at face value but will limit our ability to comment meaningfully on location, size, and type of outlet. 

## Methods
The work for this project was split into multiple Jupyter Notebooks to keep individual steps and processes distinct and separate. This was done to keep from re-running initial steps (ETL, cleaning) and to reduce the code and processing time for our analysis notebooks (hypothesis testing). The general workflow was as follows:
- [Phase 1](https://github.com/msmccann10/PP-movie-database-and-analysis/blob/main/01_IMDB_Data_Loading_and_Processing.ipynb): Download IMDB data. Inspect and clean it based on our customer's specifications. 
- [Phase 2](https://github.com/msmccann10/PP-movie-database-and-analysis/blob/main/02_TMDB_API_Pull.ipynb): Build an API call for the TMDB database. Retrieve data for 2000-2021. 
- [Phase 3](https://github.com/msmccann10/PP-movie-database-and-analysis/blob/main/03_TMDB_Data_Consolidation_Processing_EDA.ipynb): Clean TMDB.
- [Phase 4](https://github.com/msmccann10/PP-movie-database-and-analysis/blob/main/04_MYSQL_Database_Creation.ipynb): Create MySQL database using IMDB and TMDB data.
- [Phase 5](https://github.com/msmccann10/PP-movie-database-and-analysis/blob/main/05_Hypothesis_Testing.ipynb): Use MySQL database to conduct hypothesis testing. 

## Results – Hypothesis Testing 
### MPAA Rating Effect
Question:
- Null Hypothesis: MPAA rating does not affect the revenue a movie generates.
- Alternative Hypothesis: MPAA does affect the revenue a movie generates.
- Alpha: 0.05

### Genre Effect
Question:
- Null Hypothesis:
- Alternative Hypothesis:
- Alpha: 0.05

![]("images/genre tukey.png")

### Runtime Trends
Question:
- Null Hypothesis: Movie runtime (length) has not changed significantly since 2000.
- Alternative Hypothesis: Movie runtime (length) has changed significantly since 2000.
- Alpha: 0.05

### Runtime Effect
Question:
- Null Hypothesis: Move length does not affect the revenue a movie generates.
- Alternative Hypothesis: Movie length does affect the revenue a movie generates.
- Alpha: 0.05

## Recommendations
