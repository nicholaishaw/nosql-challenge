# Background
The UK Food Standards Agency evaluates various establishments across the United Kingdom and gives them a food hygiene rating. In a fictional world, I have been contracted by the editors of a food magazine, Eat Safe, Love, to evaluate some of the ratings data in order to help their journalists and food critics decide where to focus future articles.

## Part 1: Database and Jupyter Notebook Set Up
The agency provided the data in the 'establishments.json' file in the resources folder. I used the terminal to import the data into a mongo database named 'uk_food.' I named the collection 'establishments'. I copied the text I used to import my data from my terminal to a markdown cell in my notebook for ease of replication.

Once the Mongo database was set up, I started a Jupyter Notebook to manage the data:
* Imported the following libraries: PyMongo and Pretty Print (pprint).
* Created an instance of the Mongo Client.
* Confirmed that you created the database and loaded the data properly:
* Listed the databases you have in MongoDB. Confirm that uk_food is listed.
* Listed the collection(s) in the database to ensure that establishments is there.
* Found and displayed one document in the establishments collection using find_one and display with pprint.
* Assigned the establishments collection to a variable to prepare the collection for use.
  
![image](https://github.com/nicholaishaw/nosql-challenge/assets/135463220/45e007b3-6499-4764-8e26-7e473862d1e5)

**Figure 1.** *A sample document in the 'establishments' collection.*


## Part 2: Update the Database
Use NoSQL_setup_starter.ipynb for this section of the challenge.

The magazine editors have some requested modifications for the database before you can perform any queries or analysis for them. Make the following changes to the establishments collection:

An exciting new halal restaurant just opened in Greenwich, but hasn't been rated yet. The magazine has asked you to include it in your analysis. Add the following information to the database:
![image](https://github.com/nicholaishaw/nosql-challenge/assets/135463220/9e318a7d-5914-4172-9294-8b0c6356567c)

Find the BusinessTypeID for "Restaurant/Cafe/Canteen" and return only the BusinessTypeID and BusinessType fields.

Update the new restaurant with the BusinessTypeID you found.

The magazine is not interested in any establishments in Dover, so check how many documents contain the Dover Local Authority. Then, remove any establishments within the Dover Local Authority from the database, and check the number of documents to ensure they were deleted.

Some of the number values are stored as strings, when they should be stored as numbers.

Use update_many to convert latitude and longitude to decimal numbers.
Use update_many to convert RatingValue to integer numbers.

## Part 3: Exploratory Analysis
Eat Safe, Love has specific questions they want you to answer, which will help them find the locations they wish to visit and avoid.

Use NoSQL_analysis_starter.ipynb for this section of the challenge.

Some notes to be aware of while you are exploring the dataset:

RatingValue refers to the overall rating decided by the Food Authority and ranges from 1-5. The higher the value, the better the rating.
Note: This field also includes non-numeric values such as 'Pass', where 'Pass' means that the establishment passed their inspection but isn't given a number rating. We will coerce non-numeric values to nulls during the database setup before converting ratings to integers.
The scores for Hygiene, Structural, and ConfidenceInManagement work in reverse. This means, the higher the value, the worse the establishment is in these areas.
Use the following questions to explore the database, and find the answers, so you can provide them to the magazine editors.

Unless otherwise stated, for each question:

Use count_documents to display the number of documents contained in the result.

Display the first document in the results using pprint.

Convert the result to a Pandas DataFrame, print the number of rows in the DataFrame, and display the first 10 rows.

Which establishments have a hygiene score equal to 20?

Which establishments in London have a RatingValue greater than or equal to 4?

Hint: The London Local Authority has a longer name than "London" so you will need to use $regex as part of your search.

What are the top 5 establishments with a RatingValue of 5, sorted by lowest hygiene score, nearest to the new restaurant added, "Penang Flavours"?

Hint: You will need to compare the geocode to find the nearest locations. Search within 0.01 degree on either side of the latitude and longitude.

How many establishments in each Local Authority area have a hygiene score of 0? Sort the results from highest to lowest, and print out the top ten local authority areas.

Hint: You will need to use the aggregation method to answer this.

The first 5 rows of your resulting DataFrame should look something like this:

