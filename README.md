# ETL Pipeline using SQLAlchemy

## Overview

This repository contains a Jupyter Notebook that demonstrates an **ETL (Extract, Transform, Load) pipeline** using **SQLAlchemy**. The pipeline extracts data from the **JSONPlaceholder API**, transforms it, and loads it into a **MySQL database**.

## Steps in the ETL Pipeline

### 1. Extraction
- Data is extracted from the **JSONPlaceholder API**.
- The extracted data includes **nested lists**, which are processed accordingly.

### 2. Transformation
- The extracted data is transformed to match the schema of the database.
- Phone numbers are cleaned using regex:
  
  ```python
  cleaned_phone = re.sub(r'\s*x\d*$', '', user['phone'])
  ```
  
- Nested lists are transformed to extract actual values for database tables.

### 3. Loading
- A **MySQL database** is created to store the transformed data.
- Data is loaded into three tables:

## Database Schema

### **users** (Stores user information)
| Column | Type | Description |
|--------|------|-------------|
| id | Primary Key | Unique identifier |
| name | String | User's full name |
| username | String | User's username |
| email | String | User's email address |
| phone | String | Cleaned phone number |
| website | String | User's website |

### **address** (Stores user address information)
| Column | Type | Description |
|--------|------|-------------|
| id | Primary Key | Unique identifier |
| user_id | Foreign Key | References `users` table |
| street | String | Street name |
| suite | String | Suite or apartment |
| city | String | City name |
| zipcode | String | Postal code |
| latitude | Float | Geographical latitude |
| longitude | Float | Geographical longitude |

### **company** (Stores user company information)
| Column | Type | Description |
|--------|------|-------------|
| id | Primary Key | Unique identifier |
| user_id | Foreign Key | References `users` table |
| name | String | Company name |
| catchPhrase | String | Company slogan |
| bs | String | Business sector |

## SQLAlchemy Implementation
- A **SQLAlchemy session** is created for database interaction.
- A **declarative base** is defined according to the schema of the tables.
- The transformed data is successfully loaded into the **MySQL database**.

## Requirements

- **Python 3.x**
- **SQLAlchemy**
- **MySQL Server**
- **Requests**
- **JSON module**
- **Regex (re module)**

## How to Run

1. Clone this repository:
   ```sh
   git clone <repository_url>
   ```
2. Install the required dependencies:
   ```sh
   pip install sqlalchemy mysql-connector-python requests
   ```
3. Set up a MySQL database and update the database connection details in the notebook.
4. Run the **Jupyter Notebook** to execute the ETL pipeline.

## Conclusion

This project successfully demonstrates an **end-to-end ETL pipeline** using **SQLAlchemy**, handling **nested JSON data**, transforming it appropriately, and loading it into a **structured MySQL database**.
