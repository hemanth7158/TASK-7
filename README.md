
# SQLite Data Handling and Analysis using Python

## What I Do:
This code snippet demonstrates how to:
1. Connect to a SQLite database.
2. Create a table called `sales` if it doesn't already exist.
3. Insert multiple rows of sales data into the table.
4. Run a query to calculate total quantity and revenue grouped by product type.

## How I Do It:

### 1. Import Necessary Libraries:
python
import sqlite3
import pandas as pd
import matplotlib.pyplot as plt

- `sqlite3`: To create and interact with the SQLite database.
- `pandas`: For data manipulation (used later for data visualization or handling).
- `matplotlib.pyplot`: For plotting graphs if needed.

### 2. Connect to SQLite Database:
python
conn = sqlite3.connect("sales_data.db")
cursor = conn.cursor()

- Establishes a connection to a SQLite database file named `sales_data.db`.
- Creates a cursor object to execute SQL commands.

### 3. Create the Sales Table:
python
cursor.execute("""
CREATE TABLE IF NOT EXISTS sales (
    id INTEGER PRIMARY KEY AUTOINCREMENT,
    product TEXT,
    quantity INTEGER,
    price REAL
)
""")

- Ensures that the `sales` table is created with columns for ID, product name, quantity sold, and price.

### 4. Insert Data into the Table:
python
data = [
    ('Laptop',5,50000), ('Mouse',10,500), ('Keyboard',7,800), ('Monitor',3,10000),
    ('Laptop',2,52000), ('Mouse',8,450), ('Keyboard',5,850), ('Monitor',2,9800),
    ('Laptop',4,51000), ('Mouse',9,470), ('Keyboard',6,830), ('Monitor',5,9700),
    ('Laptop',3,49500), ('Mouse',6,460), ('Keyboard',8,810), ('Monitor',1,10500),
    ('Laptop',6,50500), ('Mouse',12,480), ('Keyboard',3,820), ('Monitor',4,10100)
]
cursor.executemany("INSERT INTO sales (product, quantity, price) VALUES (?, ?, ?)", data)
conn.commit()

- Prepares a list of tuples with product sales records.
- Uses `executemany()` to batch insert all rows.
- Commits the transaction to save changes in the database.

### 5. Query to Analyze Sales:
python
query = """
SELECT product,
       SUM(quantity) AS total_qty,
       SUM(quantity * price) AS revenue
FROM sales
GROUP BY product
"""

- Selects each unique product.
- Calculates the total quantity sold (`SUM(quantity)`).
- Calculates total revenue as the product of quantity and price (`SUM(quantity * price)`).
- Groups the result by product name.

## Conclusion:
This program is a simple but powerful way to manage and analyze sales data using SQLite with Python. It can be expanded further to include visualizations and advanced reporting using libraries like `pandas` and `matplotlib`.

