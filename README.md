# autoDB_normalization
Database normalization practice using SQL(1nf-3nf)


### Ticket Breakdown for SQL Project (Using MySQL Workbench)

#### Ticket 1: Copy Unnormalized Database(you will be using this throughout the assignment)

```sql
CREATE DATABASE AutomotiveDB;

USE AutomotiveDB;

CREATE TABLE UnnormalizedCars (
    CarID INT,
    CarModel VARCHAR(100),
    OwnerName VARCHAR(100),
    OwnerAddress VARCHAR(255),
    OwnerPhone VARCHAR(20),
    ServiceDates VARCHAR(255),
    ServiceDescriptions VARCHAR(255),
    TotalServiceCost DECIMAL(10, 2)
);

INSERT INTO UnnormalizedCars VALUES
(1, 'Toyota Camry', 'John Doe', '123 Elm St', '555-1234', '2021-01-10,2021-06-15', 'Oil Change,Tire Rotation', 150.00),
(2, 'Honda Accord', 'Alice Johnson', '456 Oak St', '555-8765', '2021-02-20,2021-08-30', 'Brake Inspection,Battery Replacement', 200.00),
(3, 'Ford Focus', 'Chris Evans', '789 Pine St', '555-6789', '2021-03-15', 'Transmission Repair', 500.00),
(4, 'Chevrolet Malibu', 'Emily Davis', '101 Maple St', '555-9876', '2021-04-25,2021-09-10', 'Engine Tune-Up,Alignment', 300.00),
(5, 'Nissan Altima', 'David Wilson', '202 Birch St', '555-2468', '2021-05-05,2021-11-20', 'Oil Change,Brake Replacement', 250.00),
(6, 'Hyundai Elantra', 'Susan Clark', '304 Cherry St', '555-3322', '2021-04-20,2021-10-10', 'Oil Change,Air Filter', 130.00),
(7, 'BMW 320i', 'Michael Brown', '987 Walnut St', '555-7788', '2021-02-28,2021-08-05', 'Brake Inspection,Transmission Repair', 650.00),
(8, 'Audi A4', 'Jennifer Lopez', '402 Cedar St', '555-9988', '2021-03-22,2021-09-12', 'Battery Replacement,Tire Rotation', 200.00),
(9, 'Mercedes C-Class', 'Robert King', '123 Oak St', '555-5544', '2021-05-18,2021-12-01', 'Engine Tune-Up,Alignment', 450.00),
(10, 'Volkswagen Passat', 'Emily Johnson', '456 Pine St', '555-1239', '2021-06-10,2021-11-20', 'Oil Change,Brake Replacement', 300.00);
```


**Tasks:**
1. Copy then run the provided SQL file to create the `AutomotiveDB` database and `UnnormalizedCars` table with sample data.

**Hints:**
- The table should contain columns for CarID, CarModel, OwnerName, OwnerAddress, OwnerPhone, ServiceDates, ServiceDescriptions, and TotalServiceCost.
- Ensure the data is in a single table without splitting repeating groups.

**Example Data Structure:**

| CarID | CarModel        | OwnerName     | OwnerAddress | OwnerPhone | ServiceDates       | ServiceDescriptions      | TotalServiceCost |
|-------|-----------------|---------------|--------------|------------|--------------------|--------------------------|------------------|
| 1     | Toyota Camry    | John Doe      | 123 Elm St   | 555-1234   | 2021-01-10,2021-06-15 | Oil Change,Tire Rotation  | 150.00           |
| 2     | Honda Accord    | Alice Johnson | 456 Oak St   | 555-8765   | 2021-02-20,2021-08-30 | Brake Inspection,Battery Replacement | 200.00           |
| 3     | Ford Focus      | Chris Evans   | 789 Pine St  | 555-6789   | 2021-03-15 | Transmission Repair | 500.00 |
| 4     | Chevrolet Malibu| Emily Davis   | 101 Maple St | 555-9876   | 2021-04-25,2021-09-10 | Engine Tune-Up,Alignment | 300.00 |
| 5     | Nissan Altima   | David Wilson  | 202 Birch St | 555-2468   | 2021-05-05,2021-11-20 | Oil Change,Brake Replacement | 250.00 |
| 6     | Hyundai Elantra | Susan Clark   | 304 Cherry St| 555-3322   | 2021-04-20,2021-10-10 | Oil Change,Air Filter | 130.00 |
| 7     | BMW 320i        | Michael Brown | 987 Walnut St| 555-7788   | 2021-02-28,2021-08-05 | Brake Inspection,Transmission Repair | 650.00 |
| 8     | Audi A4         | Jennifer Lopez| 402 Cedar St | 555-9988   | 2021-03-22,2021-09-12 | Battery Replacement,Tire Rotation | 200.00 |
| 9     | Mercedes C-Class| Robert King   | 123 Oak St   | 555-5544   | 2021-05-18,2021-12-01 | Engine Tune-Up,Alignment | 450.00 |
| 10    | Volkswagen Passat| Emily Johnson| 456 Pine St  | 555-1239   | 2021-06-10,2021-11-20 | Oil Change,Brake Replacement | 300.00 |

#### Ticket 2: Normalize Database to First Normal Form (1NF)

**Description:** Normalize the database to First Normal Form (1NF).

**Why?**  
First Normal Form (1NF) ensures that the values in each column are atomic (indivisible). This eliminates repeating groups and arrays in columns.

**Tasks:**
1. Create separate `Cars1NF` and `Services1NF` tables with atomic values.
2. Define primary and foreign keys to establish relationships between tables.

**Hints:**
- Atomic values mean that each piece of information is stored separately.
- Split the service dates and descriptions into separate rows.

**Example Data Structure for 1NF:**

| CarID | CarModel        | OwnerName     | OwnerAddress | OwnerPhone |
|-------|-----------------|---------------|--------------|------------|
| 1     | Toyota Camry    | John Doe      | 123 Elm St   | 555-1234   |
| 2     | Honda Accord    | Alice Johnson | 456 Oak St   | 555-8765   |

| ServiceID | CarID | ServiceDate | ServiceDescription | ServiceCost |
|-----------|-------|-------------|--------------------|-------------|
| 1         | 1     | 2021-01-10  | Oil Change         | 50.00       |
| 2         | 1     | 2021-06-15  | Tire Rotation      | 100.00      |
| 3         | 2     | 2021-02-20  | Brake Inspection   | 100.00      |

**Example structure for `Cars1NF` table:**
- CarID (Primary Key)
- CarModel
- OwnerName
- OwnerAddress
- OwnerPhone

**Example structure for `Services1NF` table:**
- ServiceID (Primary Key)
- CarID (Foreign Key)
- ServiceDate
- ServiceDescription
- ServiceCost

#### Ticket 3: Normalize Database to Second Normal Form (2NF)

**Description:** Normalize the database to Second Normal Form (2NF).

**Why?**  
Second Normal Form (2NF) removes partial dependencies; this means that all non-key attributes are fully functionally dependent on the primary key.

**Tasks:**
1. Create `Owners` table to separate owner information from car information.
2. Update `Cars2NF` table to reference `Owners` table.

**Hints:**
- Use foreign keys to link tables.
- Ensure that each non-key attribute is dependent on the whole primary key.

**Example Data Structure for 2NF:**

| OwnerID | OwnerName     | OwnerAddress | OwnerPhone |
|---------|---------------|--------------|------------|
| 1       | John Doe      | 123 Elm St   | 555-1234   |
| 2       | Alice Johnson | 456 Oak St   | 555-8765   |

| CarID | CarModel        | OwnerID |
|-------|-----------------|---------|
| 1     | Toyota Camry    | 1       |
| 2     | Honda Accord    | 2       |

**Example structure for `Owners` table:**
- OwnerID (Primary Key)
- OwnerName
- OwnerAddress
- OwnerPhone

**Example structure for `Cars2NF` table:**
- CarID (Primary Key)
- CarModel
- OwnerID (Foreign Key)

**Example structure for `Services2NF` table:**
- ServiceID (Primary Key)
- CarID (Foreign Key)
- ServiceDate
- ServiceDescription
- ServiceCost

#### Ticket 4: Normalize Database to Third Normal Form (3NF)

**Description:** Normalize the database to Third Normal Form (3NF).

**Why?**  
Third Normal Form (3NF) removes transitive dependencies; this means that non-key attributes are not only dependent on the primary key but not on other non-key attributes.

**Tasks:**
1. Create `ServiceTypes` table to separate service type information from service history.
2. Update `Services3NF` table to reference `ServiceTypes` table.

**Hints:**
- Use foreign keys to reference related tables.
- Ensure that non-key attributes depend only on the primary key and not on other non-key attributes.

**Example Data Structure for 3NF:**

| ServiceTypeID | ServiceDescription | ServiceCost |
|---------------|--------------------|-------------|
| 1             | Oil Change         | 50.00       |
| 2             | Tire Rotation      | 100.00      |

| ServiceID | CarID | ServiceDate | ServiceTypeID |
|-----------|-------|-------------|---------------|
| 1         | 1     | 2021-01-10  | 1             |
| 2         | 1     | 2021-06-15  | 2             |
| 3         | 2     | 2021-02-20  | 3             |

**Example structure for `ServiceTypes` table:**
- ServiceTypeID (Primary Key)
- ServiceDescription
- ServiceCost

**Example structure for `Services3NF` table:**
- ServiceID (Primary Key)
- CarID (Foreign Key)
- ServiceDate
- ServiceTypeID (Foreign Key)

### Insert Statements for the Final Normalized Database

Once the database is fully normalized, insert the sample data into the final tables.

```sql
-- Insert data into Owners table
INSERT INTO Owners (OwnerID, OwnerName, OwnerAddress, OwnerPhone) VALUES
(1, 'John Doe', '123 Elm St', '555-1234'),
(2, 'Alice Johnson', '456 Oak St', '555-8765'),
(3, 'Chris Evans', '789 Pine St', '555-6789'),
(4, 'Emily Davis', '101 Maple St', '555-9876'),
(5, 'David Wilson', '202 Birch St', '555-2468'),
(6, 'Susan Clark', '304 Cherry St', '555-3322'),
(7, 'Michael Brown', '987 Walnut St', '555-7788'),
(8, 'Jennifer Lopez', '402 Cedar St', '555-9988'),
(9, 'Robert King', '123 Oak St', '555-5544'),
(10, 'Emily Johnson', '456 Pine St', '555-1239');

-- Insert data into Cars2NF table
INSERT INTO Cars2NF (CarID, CarModel, OwnerID) VALUES
(1, 'Toyota Camry', 1),
(2, 'Honda Accord', 2),
(3, 'Ford Focus', 3),
(4, 'Chevrolet Malibu', 4),
(5, 'Nissan Altima', 5),
(6, 'Hyundai Elantra', 6),
(7, 'BMW 320i', 7),
(8, 'Audi A4', 8),
(9, 'Mercedes C-Class', 9),
(10, 'Volkswagen Passat', 10);

-- Insert data into ServiceTypes table
INSERT INTO ServiceTypes (ServiceTypeID, ServiceDescription, ServiceCost) VALUES
(1, 'Oil Change', 50.00),
(2, 'Tire Rotation', 100.00),
(3, 'Brake Inspection', 100.00),
(4, 'Battery Replacement', 100.00),
(5, 'Transmission Repair', 500.00),
(6, 'Engine Tune-Up', 150.00),
(7, 'Alignment', 150.00),
(8, 'Brake Replacement', 200.00);

-- Insert data into Services3NF table
INSERT INTO Services3NF (CarID, ServiceDate, ServiceTypeID) VALUES
(1, '2021-01-10', 1),
(1, '2021-06-15', 2),
(2, '2021-02-20', 3),
(2, '2021-08-30', 4),
(3, '2021-03-15', 5),
(4, '2021-04-25', 6),
(4, '2021-09-10', 7),
(5, '2021-05-05', 1),
(5, '2021-11-20', 8),
(6, '2021-04-20', 1),
(6, '2021-10-10', 6),
(7, '2021-02-28', 3),
(7, '2021-08-05', 5),
(8, '2021-03-22', 4),
(8, '2021-09-12', 2),
(9, '2021-05-18', 6),
(9, '2021-12-01', 7),
(10, '2021-06-10', 1),
(10, '2021-11-20', 8);
```

#### Test the Database with SELECT Statements

To verify the normalization, use the following SELECT statements to query the database:

```sql
-- Query the Cars2NF table to retrieve car information
SELECT * FROM Cars2NF;

-- Query the Owners table to retrieve owner information
SELECT * FROM Owners;

-- Query the Services3NF table to retrieve service history
SELECT * FROM Services3NF;

-- Query the ServiceTypes table to retrieve service type information
SELECT * FROM ServiceTypes;
```

Sure! Here's the expected output for each table after normalizing the database and inserting the data, in markdown format:

```
**Expected Output for Cars2NF Table:**

| CarID | CarModel        | OwnerID |
|-------|-----------------|---------|
|     1 | Toyota Camry    |       1 |
|     2 | Honda Accord    |       2 |
|     3 | Ford Focus      |       3 |
|     4 | Chevrolet Malibu|       4 |
|     5 | Nissan Altima   |       5 |
|     6 | Hyundai Elantra |       6 |
|     7 | BMW 320i        |       7 |
|     8 | Audi A4         |       8 |
|     9 | Mercedes C-Class|       9 |
|    10 | Volkswagen Passat|     10 |

**Expected Output for Owners Table:**

| OwnerID | OwnerName     | OwnerAddress | OwnerPhone |
|---------|---------------|--------------|------------|
|       1 | John Doe      | 123 Elm St   | 555-1234   |
|       2 | Alice Johnson | 456 Oak St   | 555-8765   |
|       3 | Chris Evans   | 789 Pine St  | 555-6789   |
|       4 | Emily Davis   | 101 Maple St | 555-9876   |
|       5 | David Wilson  | 202 Birch St | 555-2468   |
|       6 | Susan Clark   | 304 Cherry St| 555-3322   |
|       7 | Michael Brown | 987 Walnut St| 555-7788   |
|       8 | Jennifer Lopez| 402 Cedar St | 555-9988   |
|       9 | Robert King   | 123 Oak St   | 555-5544   |
|      10 | Emily Johnson | 456 Pine St  | 555-1239   |

**Expected Output for Services3NF Table:**

| ServiceID | CarID | ServiceDate | ServiceTypeID |
|-----------|-------|-------------|---------------|
|         1 |     1 | 2021-01-10  |             1 |
|         2 |     1 | 2021-06-15  |             2 |
|         3 |     2 | 2021-02-20  |             3 |
|         4 |     2 | 2021-08-30  |             4 |
|         5 |     3 | 2021-03-15  |             5 |
|         6 |     4 | 2021-04-25  |             6 |
|         7 |     4 | 2021-09-10  |             7 |
|         8 |     5 | 2021-05-05  |             1 |
|         9 |     5 | 2021-11-20  |             8 |
|        10 |     6 | 2021-04-20  |             1 |
|        11 |     6 | 2021-10-10  |             6 |
|        12 |     7 | 2021-02-28  |             3 |
|        13 |     7 | 2021-08-05  |             5 |
|        14 |     8 | 2021-03-22  |             4 |
|        15 |     8 | 2021-09-12  |             2 |
|        16 |     9 | 2021-05-18  |             6 |
|        17 |     9 | 2021-12-01  |             7 |
|        18 |    10 | 2021-06-10  |             1 |
|        19 |    10 | 2021-11-20  |             8 |

**Expected Output for ServiceTypes Table:**

| ServiceTypeID | ServiceDescription | ServiceCost |
|---------------|--------------------|-------------|
|             1 | Oil Change         |        50.00|
|             2 | Tire Rotation      |       100.00|
|             3 | Brake Inspection   |       100.00|
|             4 | Battery Replacement|       100.00|
|             5 | Transmission Repair|       500.00|
|             6 | Engine Tune-Up     |       150.00|
|             7 | Alignment          |       150.00|
|             8 | Brake Replacement  |       200.00|
```
