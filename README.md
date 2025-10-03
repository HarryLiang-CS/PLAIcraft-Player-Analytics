## 1. Introduction
### (1)Background information

### Project Outline
For this project, we are conducting our own data analysis, using data from a project conducted by UBC Computer Science researchers in The Pacific Laboratory for Artificial Intelligence (PLAI) Group. These researchers are studying how people play video games by recording play sessions on a specific MineCraft server and collecting relevant data. Our goal is to formulate a predictive question from our exploration of the datasets "players.csv" and "sessions.csv" and answer it using reading, wrangling, visualization, and classification skills that we have learnt so far in DSCI 100.

### PLAICraft
The datasets supplied to us for this project come from the PLAI group's MineCraft research server, PLAICraft. PLAICraft player data includes skill level, subscription status, demographic, and individual play session data.

### (2)Question we tried to answer
#### **Broad Question**
What player characteristics and behaviours are most predictive of subscribing to a game-related newsletter, and how do these features differ between various player types?

#### **Specific Question**
Can experience, age and played hours predict whether a player subscribes to a game-related newsletter in the PLAICraft server dataset?

### (3)Describe the dataset
#### Game player data set
This data was taken from [a research group in Computer Science at UBC](https://plai.cs.ubc.ca/). This dataset contains information about players and their game sessions collected from the PLAICraft research game server. The goal is to analyze the factors that influence players' likelihood of subscribing to the game newsletter.

**players.csv**: This data is a list of all unique players, including data about each player. According to the website, the file contains the following information:

* experience (character) = The player's experience level.
* subscribe (logical) = Subscription to the game newsletter (TRUE / FALSE)
* hashedEmail (character) = Player's Hashed email
* played_hours (numeric) = Total play time (hours)
* name (character) = Player's name
* gender (character) = Player's gender
* Age (numeric) = Player's age
  
**sessions.csv**: A list of individual play sessions by each player, including data about the session. According to the website, the file contains the following information:

* hashedEmail (character) = Player's Hashed email
* start_time (character) = Session start time (Format: DD/MM/YYYY HH:MM)
* end_time (character) = Session end time (Format: DD/MM/YYYY HH:MM)
* original_start_time (numeric) = Unix timestamp of session start
* original_end_time (numeric) = Unix timestamp of session end

## 2. Methods & Results
### K-Nearest Neighbors (KNN) Classification. 
We are using KNN classification to predict whether a new player entering the game will subscribe to the PLAICraft newsletter based on their input for the chosen variables (experience, Age, played_hours). 

This method of classification calculates the distance between a new data point and its K-nearest neighbors and assigns the majority class as the prediction result. The steps are as follows:
* Load in R packages and datasets
* Clean the dataset:
    * Convert `subscribe` into a factor variable
    * Convert `experience` into numeric variables
    * Handle missing values
    * Standardize the `played_hours` and `Age` data
    * Remove players whose `played_hours` is 0, as they do not contribute meaningful game behaviour data
    * Drop hashedEmail and name as they’re not relevant for prediction
* Visualize the clean data and explore the relationship between each variable with subscription status
* Split the data into training and testing by 70/30
* Build training model
* Use cross-validation on training data to find the best K for our classification model
* Retrain model with chosen K
* Calculate accuracy of model
* Predict a new player's class label (subscribed? true or false) using our model