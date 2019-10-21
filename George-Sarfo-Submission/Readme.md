Author: George Sarfo
Desc: ETL Pipeline for POS Product Matching
Date: 10/21/2019

Details


1. Assume a DEV environment
2. Two Modules are used INSIDE the main program
3. The Modular Approach allows for other users to call or import the modules and use the functions in parallel

4. Not much logging was done - can be done when productionalized and alerts (EMAIL and SMS) incorporated
5. No config File was used - in a Production environment, config file or AWS SSMP can be used to hold necessary parameters to be passed
6. An execution or orchestration tool (luigi or airflow) will be used to schedule and run the main scripts
7. Main script can be invoked using a Lambda function upon the arrival of a new pos_json_file
8. Historical records of each pos_json_file is kept with a timestamp - to allow for record keeping and reprocessing when need be
9. Packages required are imported as part of script - in a production env requirements.txt will be used 

High Level Logic and Flow

Main Program imports the db_connection module and the fuzzy matching module

main program calls fuzzy matching module which contains the main_brain function that does the matching and final output

the final output contains the pos_product, matched_iheart_jane_product, matched_jane_product_id and the fuzzy_match_score

Fuzzy Scoring 

Fuzzy Scoring uses Levenstein distance that allows for two long strings of words to matched based on similarity of the words in each string,

it does this by calculating the Levenstein distance between the words of each string and calculating a score to see if the two strings are a 
close match

in this matching, we use a threshold of 70 which is passed as part of the main program - can be passed using config file or AWS SSMP

All POS product names and categories matching those in the Iheart_Jane_DB are returned and their corresponding jane_product_ID is returned
as a CSV (final_matches_output.csv)
