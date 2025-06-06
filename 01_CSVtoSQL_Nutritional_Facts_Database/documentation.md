USDA Nutrition Data Importer
A Python script to import USDA nutrition data from CSV files into a MySQL database. Handles data cleaning, NULL value conversion, and provides a clean database schema for nutrition analysis.
Features

Data Cleaning: Automatically handles malformed numeric values, removes commas, and strips whitespace
NULL Value Handling: Converts empty strings, 'N/A', '--', and other placeholder values to proper SQL NULL
Progress Tracking: Real-time import progress with row count updates
Data Validation: Sample data verification after import completion
Error Handling: Comprehensive error handling for database and file operations

Requirements

Python 3.6+
MySQL Server
Required Python packages:
mysql-connector-python


Installation

Clone this repository
Install required packages:
bashpip install mysql-connector-python

Set up your MySQL database and update configuration

Configuration
Update the database configuration in the script:
pythonDB_CONFIG = {
    'host': 'localhost',
    'user': 'your_username',
    'password': 'your_password',
    'database': 'usda',
    'auth_plugin': 'mysql_native_password'
}
Update the CSV file path:
pythonCSV_FILE = 'path/to/your/USDA.csv'
CSV Format
The script expects a CSV file with the following columns:

Description: Food item description
Calories: Caloric content per 100g
Protein: Protein content in grams per 100g
TotalFat: Total fat content in grams per 100g
Carbohydrate: Carbohydrate content in grams per 100g
Sugar: Sugar content in grams per 100g

Database Schema
The script creates a nutrition table with the following structure:
sqlCREATE TABLE nutrition (
    id INT AUTO_INCREMENT PRIMARY KEY,
    description VARCHAR(255),
    calories FLOAT,
    protein FLOAT,
    total_fat FLOAT,
    carbohydrate FLOAT,
    sugar FLOAT
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4
Usage
Run the script directly:
bashpython3 usda_importer.py
The script will:

Connect to the MySQL database
Drop and recreate the nutrition table
Import all CSV data with proper data type conversion
Display progress updates during import
Show sample imported data for verification

Data Processing
The converter_float() function handles various data quality issues:

Removes commas from numeric values
Strips whitespace
Converts empty strings and placeholder values ('N/A', 'na', '--', 'null') to SQL NULL
Handles scientific notation (e.g., 1.23e-4)
Returns None for any values that cannot be converted to float

Error Handling
The script includes comprehensive error handling for:

MySQL connection issues
File reading errors
Data conversion problems
SQL execution errors

All errors are logged to console with descriptive messages.
License
This project is open source and available under the MIT License.
