# SQL Music Store Analysis

## Overview

The **SQL Music Store Analysis** project aims to analyze and manage a music store's inventory, sales, and customer data using SQL queries. The system uses **PostgreSQL** as the database management system and **Admin4** for database administration. The project demonstrates the use of SQL for handling data operations in the context of a music store, including analyzing sales trends, inventory management, and customer behavior.

## Features

- **Inventory Management**: Track music albums, genres, artists, and available stock.
- **Sales Analysis**: Analyze sales trends, total revenue, and product popularity.
- **Customer Data**: Manage customer information, their purchase history, and interactions with the store.
- **Reporting**: Generate reports on total sales, top-selling albums, and most frequent customers.

## Technologies Used

- **PostgreSQL**: Relational database used to store and manage data.
- **Admin4**: Admin interface used to manage the PostgreSQL database and perform SQL queries.

## Database Schema

The following tables are used in the database:

1. **Albums**: Stores details of music albums.
   - `album_id (PK)`: Unique identifier for the album.
   - `title`: Name of the album.
   - `artist`: Artist of the album.
   - `genre`: Genre of the album.
   - `price`: Price of the album.
   - `stock`: Number of albums available in the store.

2. **Customers**: Stores customer details.
   - `customer_id (PK)`: Unique identifier for each customer.
   - `name`: Name of the customer.
   - `email`: Email address of the customer.
   - `phone`: Phone number of the customer.

3. **Sales**: Records each sale transaction.
   - `sale_id (PK)`: Unique identifier for each sale.
   - `customer_id (FK)`: The customer who made the purchase.
   - `album_id (FK)`: The album purchased.
   - `quantity`: Number of albums purchased.
   - `sale_date`: Date of the sale.

4. **Genres**: Stores music genre details.
   - `genre_id (PK)`: Unique identifier for the genre.
   - `genre_name`: Name of the genre (e.g., Rock, Pop).

## Setup and Installation

### 1. Clone the Repository

```bash
git clone https://github.com/yourusername/sql-music-store-analysis.git
cd sql-music-store-analysis
```

### 2. Install PostgreSQL

If you haven't installed PostgreSQL yet, you can download and install it from the official website:  
[PostgreSQL Download](https://www.postgresql.org/download/)

### 3. Set Up Database

1. Install **Admin4** or any other PostgreSQL administration tool of your choice.
2. Create a database named `music_store`:

```bash
psql -U postgres
CREATE DATABASE music_store;
```

3. Run the SQL scripts in the `database-schema.sql` file to create the necessary tables and schema for the music store.

### 4. Configure Database Connection

In the project, update your connection details in the config files if applicable to match your PostgreSQL instance (e.g., username, password, host, database name).

### 5. Run SQL Queries

Once the database is set up, you can use **Admin4** to interact with your PostgreSQL database. Execute the SQL queries in `queries.sql` to perform various data analysis tasks, such as generating sales reports, analyzing top-selling albums, and more.

## Example Queries

- **Get total revenue for each album:**

```sql
SELECT album_id, SUM(price * quantity) AS total_revenue
FROM sales
JOIN albums ON sales.album_id = albums.album_id
GROUP BY album_id;
```

- **List top 5 selling albums:**

```sql
SELECT title, SUM(quantity) AS total_sold
FROM sales
JOIN albums ON sales.album_id = albums.album_id
GROUP BY title
ORDER BY total_sold DESC
LIMIT 5;
```

- **Get customers who purchased the most albums:**

```sql
SELECT name, COUNT(DISTINCT album_id) AS albums_purchased
FROM sales
JOIN customers ON sales.customer_id = customers.customer_id
GROUP BY name
ORDER BY albums_purchased DESC
LIMIT 5;
```

## Contributing

Feel free to fork this repository and submit pull requests. If you find any issues or have suggestions for improvements, please open an issue.
