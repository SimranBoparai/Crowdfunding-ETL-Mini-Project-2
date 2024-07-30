# Table of Contents
- [Table of Contents](#table-of-contents)
- [Project Discription](#project-discription)
- [Prerequisites](#prerequisites)
  - [Installation](#installation)
  - [Repository Setup:](#repository-setup)
  - [Git Bash Command Example](#git-bash-command-example)
- [Repository Structure](#repository-structure)
- [Project Instructions](#project-instructions)
  - [PART 1: Create the Category and Subcategory DataFrames](#part1create-the-category-and-subcategory-dataframes)
    - [ Category DataFrame](#category-dataframe)
    - [ Subcategory DataFrame](#subcategory-dataframe)
  - [PART 2: Create the Campaign DataFrames](#part2create-the-campaign-dataframes)
  - [PART 3: Create the Contacts DataFrame](#part-3-create-the-contacts-dataframe)
    - [Option 1: Use Python Dictionary Methods](#option-1-use-python-dictionary-methods)
  - [PART 4: Create an ERD, Postgres Database, and Table Schema](#part-4-create-an-erd-postgres-database-and-table-schema)
- [Example Code](#example-code)
  - [PART 1 Example:](#part-1-example)
  - [PART 2 Example:](#part-2-example)
  - [PART 3 Example:](#part-3-example)
  - [PART 4 Example:](#part-4-example)
- [Acknowledgements](#acknowledgements)


# Project Discription 
This project involves building an ETL (Extract, Transform, Load) pipeline using Python, Pandas, and Python dictionary methods or regular expressions to process data from Excel files. The processed data will be saved as CSV files, which will be used to create an ERD and table schema by uploading data into a Postgres database. 


# Prerequisites
Before working on the Crowdfunding ETL Project, ensure you complete the following requirements:

## Installation 
- Install VS Code, Python, and pgAdmin on your machine (can use Jupyter Notebook)
- Import Pandas, Numpy, and json 
- Create a new repository called 'Crowdfunding_ETL' in GitHub with README and .gitignore file.

## Repository Setup:
  - Create a new repository called 'Crowdfunding_ETL' in GitHub with a README file
  - Copy the SSH key in GitHub
  - Navigate into the working directory 
  - Clone SSH key in directory
    - Import the starter code and resources folder into the directory
    - Create a folder called 'Images' for all of the pgAdmin screenshots 
  - Git add, commit, and push changes into the repository

## Git Bash Command Example
Navigate into a working directory. 
```
git clone (add you ssh key)
cd 'Crowdfunding_ETL'
mkdir 'Images'
git add .
git commit -m "Pushing challenge work"
git push 
```


# Repository Structure
- Crowdfunding_ETL
    - Images
        - Campaign Schema Table
        - Category Schema Table
        - Contacts Schema Table
        - Crowdfunding_db ERD
        - Crowdfunding_db Schema Table pt1
        - Crowdfunding_db Schema Table pt2
        - Subcategory Schema Table
    - Resources
        - crowdfunding.xlsx
        - contacts.xlsx
        - category.csv
        - subcategory.csv
        - campaign.csv
        - contacts.csv
    - crowdfunding_db_schema.sql
    - ETL_Mini_Project_GKaur_Starter_Code.ipynb
 - README.md
 - gitignore
 - LICENSE
 - .git


# Project Instructions
Ensure you have downloaded the starter code and resources files to start the project.

The project is separated into four parts:

- Part 1: Create the Category and Subcategory DataFrames
  - Category DataFrame
  - Subcategory DataFrame
- Part 2: Create the Campaign DataFrames
- Part 3: Create the Contacts DataFrame
  - Option 1: Use Python Dictionary Methods
- Part 4: Create an ERD, Postgres Database, and Table Schema
        
## PART 1: Create the Category and Subcategory DataFrames
Open the ```ETL_Mini_Project_Starter_Code.ipynb``` starter code in VS Code or Jupyter Notebook and complete the following steps to the dataframes.  

###  Category DataFrame 
-  Extract data from ```crowdfunding.xlsx```
- Transform data to create a DataFrame with:
  
  - ```category_id```: Sequential entries from 'cat1' to 'catn'.
  - ```category```: Category titles.
- Export the DataFrame as ```category.csv```.

###  Subcategory DataFrame 
-  Extract data from ```crowdfunding.xlsx```
- Transform data to create a DataFrame with:
  
  - ```subcategory_id```: Sequential entries from 'subcat1' to 'subcatn'.
  - ```subcategory```: Category titles.
- Export the DataFrame as ```subcategory.csv```.

## PART 2: Create the Campaign DataFrames

- Extract data from ```crowdfunding.xlsx```
- Transform data to create a DataFrame with:
  
  - ```cf_id```
  - ```category_id```
  - ```company_name```
  - ```blurb``` (renamed to description)
  - ```goal``` (converted to float)
  - ```pledged``` (converted to float)
  - ```outcome```
  - ```backers_count```
  - ```country```
  - ```currency```
  - ```launched_at``` (renamed to launch_date and converted to datetime format)
  - ```deadline``` (renamed to end_date and converted to datetime format)
  - ```category_id``` (unique identification numbers matching the category_id in the Category DataFrame)
  - ```subcategory_id``` (unique identification numbers matching the subcategory_id in the Subcategory DataFrame)
- Export the DataFrame as ```campaign.csv```.

## PART 3: Create the Contacts DataFrame
### Option 1: Use Python Dictionary Methods
- Import ```contacts.xlsx``` into a DataFrame.
- Iterate through the DataFrame and convert each row to a dictionary.
  - Extract dictionary values using a Python list comprehension.
  - Add the values for each row to a new list.
- Create a new DataFrame with the extracted data.
- Split the ```name``` column into ```first_name``` and ```last_name```.
- Clean and export the DataFrame as ```contacts.csv```.

## PART 4: Create an ERD, Postgres Database, and Table Schema
- Create an ERD (Entity Relationship Diagram) using the CSV files.
- Create a new Postgres database, name ```crowdfunding_db```
- Using the ERD and schema, create the tables in the correct order to accommodate the foreign keys. 
- Import each CSV file into its corresponding SQL Table.
- Run a ```SELECT``` statement for each table to verify that the data is correct.
- Save the database schema as a Postgres file named ```crowdfunding_db_schema.sql```. 


# Example Code
## PART 1 Example:

```VS Code
# Assign the category and subcategory values to category and subcategory columns.

crowdfunding_info_df[['category', 'subcategory']] = crowdfunding_info_df['category & sub-category'].str.split('/', expand=True)
crowdfunding_info_df
```

## PART 2 Example:
```VS Code
# Rename the blurb, launched_at, and deadline columns.

updated_columns = {"blurb": "description",
                    "launched_at": "launched_date", 
                    "deadline": "end_date"
                    }
campaign_df = campaign_df.rename(columns = updated_columns)
campaign_df
```

## PART 3 Example:
```VS Code
# Iterate through the contact_info_df and convert each row to a dictionary.

dict_values = []

for i, row in contact_info_df.iterrows():
    data = row['contact_info']
    converted_data = json.loads(data)
    row_values = [value for key, value in converted_data.items()]
    dict_values.append(row_values)

# Print out the list of values for each row.
print(dict_values)
```

## PART 4 Example:
```pg Admin
# Create a table schema and import the data using the ```contacts.csv``` file in pgAdmin.

DROP TABLE IF EXISTS contacts;

CREATE TABLE contacts(
    contact_id INT NOT NULL,
        first_name VARCHAR(50) NOT NULL,
    last_name VARCHAR(50) NOT NULL,
    email VARCHAR(50) NOT NULL,
    CONSTRAINT pk_contacts PRIMARY KEY (contact_id)
);

SELECT * 
FROM contacts;
```


# Acknowledgements
I want to mention the following individuals and resources for their assistance and support throughout this assignment: 
- Study group members
    - Omid Khan - omidk414@gmail.com - omidk414
    - Evan Wall - - ewall@escoffier.edu - Ewall24
- Xpert Learning Assistant and ChatGPT
- Python - List Comprehension (https://www.w3schools.com/python/python_lists_comprehension.asp)
