# Restaurant Recommender Chatbot

Using the recommending power of the ALS model on the Databricks platform, we will use information such as restaurant reviews and your prior reviews to recommend restaurants for you or your group via a chatbot
If there are any questions please feel free to refer to the website at: 

http://54.237.7.35/ (May have lost domain)

## Data Prep Steps
- Pull Data from kaggle 
- Run Data though the several data cleaning notebooks provided. 
## General
- Create a Lex Bot using the v1 console, ours is called FoodFinder.
- Connect this lex bot to blah bot 
- Connect the blah bot to the website
Create an S3 bucket
## ALS Model Intent
- Upload cleaned data to data bricks 
- Construct and tune and an ALS model (See Code) 
- Save the top three suggestion names for each user to MySQL(See Code) 
- In Lambda Function FindFood, call the data for each user (See Doc)
- Configure Lex box like below
    - Sample Utterances:
    - Where should I eat this time
    - What can you recommend for me
    - What would I like
- Slots Needed:
    - I am happy to help. What is your user_id?
    - user_id from AMAZON.AlphaNumeric
- Remember to attach the lambda function to the fulfillment section 
## LeaveReview Intent 
- The LeaveReview Intent sends slots to the LeaveReview Lambda Function (included in separate file), which writes the information to the final row in the 'new_reviews.csv' in the 'frankecfood' S3 bucket. The breakdown of the utterance and slots are included below.
- Sample Utterances:
    - Leave a Review
    - Review a Restaurant
    - Roast a Restaurant 
    - Review
- Slots Needed:
    - What is your user_ID?
    - User_ID from AMAZON.AlphaNumeric
    - On a scale of 1-5 how much did you like this restaurant?
    - Review from AMAZON.AlphaNumeric
    - Which restaurant is this review for?
    - Restaurant_Name  from AMAZON AlphaNumeric
    - What date is your review for?
    - Date  from AMAZON Date
## Make a General Recommendation Intent 
- The general recommendation intent will acquire the desired genre of food from the user such as Burgers, Asian, Sushi, or Bar and filter a static table hosted by the MySQL server that will retrieve a list of 5 restaurants that serve that genre of food and have 4 or 5 star ratings. The Lex Bot acquires the genre name and send it to the Lambda function which will then handle the interactions with the MySQL table.
- Sample Utterances
    - What do you suggest
    - Give me some restaurant ideas
- Slot needed
    - What kind of food would you like?
    - Genre from AMAZON.AlphaNumeric
