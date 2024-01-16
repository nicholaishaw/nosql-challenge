# Background
The UK Food Standards Agency evaluates various establishments across the United Kingdom and gives them a food hygiene rating. In a fictional world, I have been contracted by the editors of a food magazine, Eat Safe, Love, to evaluate some of the ratings data in order to help their journalists and food critics decide where to focus future articles.

## Part 1: Database and Jupyter Notebook Set Up
The agency provided the data in the 'establishments.json' file in the resources folder. I used the terminal to import the data into a Mongo database named 'uk_food.' I named the collection 'establishments'. I copied the text I used to import my data from my terminal to a markdown cell in my notebook for ease of replication.

Once the Mongo database was created and the dataset was imported, I set up a Jupyter Notebook to manage the data. The following work was performed in the NoSQL_setup.ipynb jupyter file.
* Imported the following libraries: PyMongo and Pretty Print (pprint).
* Created an instance of the Mongo Client.
* Confirmed that I created the database and loaded the data properly
* Listed the databases I have in MongoDB and confirmed that 'uk_food' is listed.
* Listed the collection(s) in the database to ensure that the collection 'establishments' is there.
* Found and displayed one document in the establishments collection using find_one and display with pprint.
* Assigned the establishments collection to a variable to prepare the collection for use.
  
![image](https://github.com/nicholaishaw/nosql-challenge/assets/135463220/45e007b3-6499-4764-8e26-7e473862d1e5)

**Figure 1.** *A sample document in the 'establishments' collection.*


## Part 2: Update the Database
Before I can perform any queries or analyses, the magazine editors requested four modifications for the database. The modifications to the database were performed in the NoSQL_setup.ipynb jupyter file. I made the following changes to the establishments collection:

1. An exciting new halal restaurant just opened in Greenwich, but hasn't been rated yet. The magazine has asked me to include it in your analysis. I added the following information to the database:

![image](https://github.com/nicholaishaw/nosql-challenge/assets/135463220/9e318a7d-5914-4172-9294-8b0c6356567c)

2. The new halal restaurant does not possess a business ID. To fix this, I first found the BusinessTypeID for "Restaurant/Cafe/Canteen" values in the database. Then, I updated the halal restaurant's BusinessTypeID value based on the BusinessTypeID I found above.

3. The magazine is not interested in any establishments in Dover, so I checked how many documents contain the Dover Local Authority. Then, I removed any establishments within the Dover Local Authority from the database, and checked the number of documents to ensure they were deleted.

4. Some of the number values are stored as strings, when they should be stored as numbers.<br>
   </br>4a. I used update_many to convert latitude and longitude to decimal numbers.<br>
   </br>4b. I used update_many to convert RatingValue to integer numbers.

## Part 3: Exploratory Analysis
The magazine has specific questions they want me to answer, which will help them find the locations they wish to visit and avoid. **The following analyses were completed in the NoSQL_analysis.ipynb jupyter file.**

Some notes to be aware when exploring the dataset:

* The RatingValue field refers to the overall rating decided by the Food Authority and ranges from 1-5. The higher the value, the better the rating.
  - **Note:** This field also includes non-numeric values such as 'Pass', where 'Pass' means that the establishment passed their inspection but isn't given a number rating. I will coerce non-numeric values to nulls during the database setup before converting ratings to integers.

* The scores for Hygiene, Structural, and ConfidenceInManagement work in reverse. This means, the higher the value, the worse the establishment is in these areas.
Use the following questions to explore the database, and find the answers, so you can provide them to the magazine editors.

The magazine wanted me to find the answers to the following questions:

* Which establishments have a hygiene score equal to 20?
* Which establishments in London have a RatingValue greater than or equal to 4?
* What are the top 5 establishments with a RatingValue of 5, sorted by lowest hygiene score, nearest to the new restaurant added, "Penang Flavours"?
* How many establishments in each local authority area have a hygiene score of 0? The results should be sorted from highest to lowest, and the top ten local authority areas should be printed. *The output will be in the form of a pandas dataframe.*

![image](https://github.com/nicholaishaw/nosql-challenge/assets/135463220/511a780f-edc8-40e5-87bb-4d495adf1337)

**Figure 2.** *Pandas dataframe containing the establishments in each local authority that have a hygiene score of 0. Only the top ten results are displayed.*
