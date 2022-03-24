# Final-Project-

## Presentation

#### Selected Topic: Auto Insurance Claims
#### Why?: From, https://insurancefraud.org/fraud-stats/, "Insurance fraud steals at least $80 billion every year from American consumers. (Coalition Against Insurance Fraud is working to update this figure in 2022)."
#### Source Data: From Kaggle.com, https://www.kaggle.com/buntyshah/auto-insurance-claims-data
#### Google Slides: https://docs.google.com/presentation/d/1y_k0o3JL7F41ck7JR_ZUZAkdtDhq-rUcgMgWNbOPW1Q/edit#slide=id.p 3/22/2022
#### Questions to Answer: 

##### Exploratory Data Analysis Questions (Pandas, Dashboards, i.e. Tableau/PowerPoint)

- Average months as a customer?
- Average age of customers?
- Policy annual premiums between genders? Between ages?
- Incident severity between genders? Between ages?
- Location based insurance statistics
- Bias in claims per input feature such as auto make and model

##### Machine Learning Questions

- What input features provide the greatest determination in insurance fraud detection?
- Which machine learning model will be most appropriate for a dataset of 40 columns with varying data types? Which columns could be dropped?
- Will our insurance dataset need binning for categorical values that have a large number of unique values?
- Are the categorical variables' unique values distributed relatively evenly?

## GitHub Protocol

#### Communication: Slack, GitBash comments, and GitHub request comments.

#### Individal Branches: 1 or more branches for each team member:
- Team Members are: Jason Mueller, Shazar Satar , and Derek Huggens.
- Each team member must have at least four commits for the duration of each segment.

## Machine Learning Model

#### Team members must present a provisional machine learning model that stands for the final machine learning model with the following abilities:
- Takes in data from the provisional database.
- Outputs label(s) for the input data.

This can be seen in our branch "ML_Model_JEM" which uses the following Python libraries to complete the ML rubric requirements for both our Random Forest and Neural Network models:
  - sklearn
  - pandas
  - tensorflow/keras
  - sqlalchemy
  - psycopg2

### Preliminary Preprocessing of ML Models:

#### Data Preprocessing: 
Firstly, we had to load the database into a notebook by connecting to PostgreSQL using psycopg2. Once connected, the database was queried and the columns with values were fetched and passed into a DataFrame. Columns with too many distinct values (some had 900+) were dropped. Datatypes were investigated and any columns that were "object" but held floats were converted using `.astype`. Our "fraud_reported" that contained "Y" and "N" strings were converted to "0" and "1." The features array was then created as all columns stored as "X_df" and the target variable "fraud_reported," was excluded. Another DataFrame was created to hold categorical columns with the "object" datatype and then be processed with `.index` and `.tolist()`. The number of unique values in each categorical column was accessed. From here, OneHotEncoder was used to fit and transform the categorical variable list into unique value columns. Finally, the encoded DataFrame was merged to the original features DataFrame "X_df," and the original categorical "object" type columns were dropped.

#### Feature Selection: 
As described above, columns with too many distinct values were dropped, and categorical columns of "object" datatype were encoded into uniquely identifiable columns and merged into the master feature DataFrame "X_df."

#### Training/Testing Sets: 
Training and Testing sets were split and scaled where "y" contained the target variable values of the "fraud_reported" column and "X" contained the values of the "X_df" DataFrame. `train_test_split` was used for "X" and "y", with a random_state of 78. `StandardScaler()` was used to `.fit()` and `.transform()` the training and testing data.

#### Model Choice Reasoning: 
Supervised machine learning models Random Forest and a Neural Network were chosen because of the complexity of our features and the fact that vehicle fraud being reported as a "Yes" or "No" prediction is a binary classification problem.

## Database

#### Team members must present a provisional database that stands in for the final database and accomplishes the following:
- Sample data mimics the expected final database structure or schema.
- The draft machine learning model is connected to the provisional database.

This can be seen in our branch "postgresql_database_branch." Our database branch contains a saved .png of our Entity Relationship Diagram (ERD) or Entity Relationship Model as well as our .sql file that contains code that created the table that was required to be able to import our .csv dataset into PostgreSQL. Additional .png screenshots of the PostgreSQL database were included to show that the database could be queried. Within the "ML_Model_JEM" branch, one can see the code required to connect to the database, and the necessary code to load the database into memory and then be stored in a DataFrame for the ML models.

Note: The Primary Key of our database was constrained to one column "policy_number" but was later deleted entirely as it did not provide use to our ML models nor did a primary key allow the ability of our REST API (using Node.js, Express.js) to GET or POST our HTML form data (since "policy_number" was not included in the form). There are communication constraints in place with PostgreSQL where you cannot insert HTML form data into a database without a value for a table's primary key.

# Dashboard

#### Team members must present a Storyboard on Google Slide(s) 
(https://docs.google.com/presentation/d/1y_k0o3JL7F41ck7JR_ZUZAkdtDhq-rUcgMgWNbOPW1Q/edit#slide=id.p)

Tools used to create final dashboard:
  - HTML
  - CSS
  - Javascript (Node.js, Express.js, REST, Flask)
  - Tableau
  - Docker (Metabase)
  - Power BI
Description of interactive element(s):
  - HTML Form
  - Tableau Story with hovering elements
  - Metabase "X-Ray" Dashboard with hovering elements
  - Power BI shareable published charts with hovering elements
  - Website fetches JSON data, logs it, and then a HTML table is built using a for loop to populate rows into respective table headers using dot-notation.
