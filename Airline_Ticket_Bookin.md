# Airline Ticketing System

## Query : Create Table Passenger

```sql
CREATE TABLE Passenger (
    ->     Passenger_ID INT PRIMARY KEY,
    ->     Name VARCHAR(100) NOT NULL,
    ->     Gender VARCHAR(10),
    ->     Date_of_Birth DATE,
    ->     Phone VARCHAR(15),
    ->     Email VARCHAR(100),
    ->     Passport_No VARCHAR(20) UNIQUE
    -> );
    DESC Passenger;
```

## Output :

```sql
+---------------+--------------+------+-----+---------+-------+
| Field         | Type         | Null | Key | Default | Extra |
+---------------+--------------+------+-----+---------+-------+
| Passenger_ID  | int(11)      | NO   | PRI | NULL    |       |
| Name          | varchar(100) | NO   |     | NULL    |       |
| Gender        | varchar(10)  | YES  |     | NULL    |       |
| Date_of_Birth | date         | YES  |     | NULL    |       |
| Phone         | varchar(15)  | YES  |     | NULL    |       |
| Email         | varchar(100) | YES  |     | NULL    |       |
| Passport_No   | varchar(20)  | YES  | UNI | NULL    |       |
+---------------+--------------+------+-----+---------+-------+
```

## Query : Create Table Airline

```sql
CREATE TABLE Airline (
    ->     Airline_ID INT PRIMARY KEY,
    ->     Airline_Name VARCHAR(100) NOT NULL,
    ->     Contact_Number VARCHAR(15)
    -> );
    DESC Airline;
```

## Output :

```sql
+----------------+--------------+------+-----+---------+-------+
| Field          | Type         | Null | Key | Default | Extra |
+----------------+--------------+------+-----+---------+-------+
| Airline_ID     | int(11)      | NO   | PRI | NULL    |       |
| Airline_Name   | varchar(100) | NO   |     | NULL    |       |
| Contact_Number | varchar(15)  | YES  |     | NULL    |       |
+----------------+--------------+------+-----+---------+-------+
```

## Query : Create Table Airport

```sql
CREATE TABLE Airport (
    ->     Airport_ID INT PRIMARY KEY,
    ->     Airport_Name VARCHAR(100) NOT NULL,
    ->     City VARCHAR(50),
    ->     Country VARCHAR(50)
    -> );
    DESC Airport;
```

## Output :

```sql
+--------------+--------------+------+-----+---------+-------+
| Field        | Type         | Null | Key | Default | Extra |
+--------------+--------------+------+-----+---------+-------+
| Airport_ID   | int(11)      | NO   | PRI | NULL    |       |
| Airport_Name | varchar(100) | NO   |     | NULL    |       |
| City         | varchar(50)  | YES  |     | NULL    |       |
| Country      | varchar(50)  | YES  |     | NULL    |       |
+--------------+--------------+------+-----+---------+-------+
```

## Query : Create Table Aircraft

```sql
CREATE TABLE Aircraft (
    ->     Aircraft_ID INT PRIMARY KEY,
    ->     Model VARCHAR(100),
    ->     Total_Seats INT,
    ->     Airline_ID INT,
    ->     FOREIGN KEY (Airline_ID) REFERENCES Airline(Airline_ID)
    -> );
    DESC Aircraft;
```

## Output :

```sql
+-------------+--------------+------+-----+---------+-------+
| Field       | Type         | Null | Key | Default | Extra |
+-------------+--------------+------+-----+---------+-------+
| Aircraft_ID | int(11)      | NO   | PRI | NULL    |       |
| Model       | varchar(100) | YES  |     | NULL    |       |
| Total_Seats | int(11)      | YES  |     | NULL    |       |
| Airline_ID  | int(11)      | YES  | MUL | NULL    |       |
+-------------+--------------+------+-----+---------+-------+
```

## Query : Create Table Flight

```sql
CREATE TABLE Flight (
    ->     Flight_ID INT PRIMARY KEY,
    ->     Flight_Number VARCHAR(20) NOT NULL,
    ->     Airline_ID INT,
    ->     Source_Airport_ID INT,
    ->     Destination_Airport_ID INT,
    ->     Departure_Time DATETIME,
    ->     Arrival_Time DATETIME,
    ->     Aircraft_ID INT,
    ->     FOREIGN KEY (Airline_ID) REFERENCES Airline(Airline_ID),
    ->     FOREIGN KEY (Source_Airport_ID) REFERENCES Airport(Airport_ID),
    ->     FOREIGN KEY (Destination_Airport_ID) REFERENCES Airport(Airport_ID),
    ->     FOREIGN KEY (Aircraft_ID) REFERENCES Aircraft(Aircraft_ID)
    -> );
    DESC Flight;
```

## Output :

```sql
+------------------------+-------------+------+-----+---------+-------+
| Field                  | Type        | Null | Key | Default | Extra |
+------------------------+-------------+------+-----+---------+-------+
| Flight_ID              | int(11)     | NO   | PRI | NULL    |       |
| Flight_Number          | varchar(20) | NO   |     | NULL    |       |
| Airline_ID             | int(11)     | YES  | MUL | NULL    |       |
| Source_Airport_ID      | int(11)     | YES  | MUL | NULL    |       |
| Destination_Airport_ID | int(11)     | YES  | MUL | NULL    |       |
| Departure_Time         | datetime    | YES  |     | NULL    |       |
| Arrival_Time           | datetime    | YES  |     | NULL    |       |
| Aircraft_ID            | int(11)     | YES  | MUL | NULL    |       |
+------------------------+-------------+------+-----+---------+-------+
```

## Query : Create Table Booking

```sql
CREATE TABLE Booking (
    ->     Booking_ID INT PRIMARY KEY,
    ->     Passenger_ID INT,
    ->     Flight_ID INT,
    ->     Booking_Date DATETIME,
    ->     Seat_Number VARCHAR(5),
    ->     Class VARCHAR(20),
    ->     Status VARCHAR(20),
    ->     FOREIGN KEY (Passenger_ID) REFERENCES Passenger(Passenger_ID),
    ->     FOREIGN KEY (Flight_ID) REFERENCES Flight(Flight_ID)
    -> );
    DESC Booking;
```

## Output :

```sql
+--------------+-------------+------+-----+---------+-------+
| Field        | Type        | Null | Key | Default | Extra |
+--------------+-------------+------+-----+---------+-------+
| Booking_ID   | int(11)     | NO   | PRI | NULL    |       |
| Passenger_ID | int(11)     | YES  | MUL | NULL    |       |
| Flight_ID    | int(11)     | YES  | MUL | NULL    |       |
| Booking_Date | datetime    | YES  |     | NULL    |       |
| Seat_Number  | varchar(5)  | YES  |     | NULL    |       |
| Class        | varchar(20) | YES  |     | NULL    |       |
| Status       | varchar(20) | YES  |     | NULL    |       |
+--------------+-------------+------+-----+---------+-------+
```

## Query : Create Table Payment

```sql
CREATE TABLE Payment (
    ->     Payment_ID INT PRIMARY KEY,
    ->     Booking_ID INT UNIQUE,
    ->     Payment_Date DATETIME,
    ->     Amount DECIMAL(10,2),
    ->     Payment_Method VARCHAR(50),
    ->     Payment_Status VARCHAR(20),
    ->     FOREIGN KEY (Booking_ID) REFERENCES Booking(Booking_ID)
    -> )
    DESC Payment;
```

## Output :

```sql
+----------------+---------------+------+-----+---------+-------+
| Field          | Type          | Null | Key | Default | Extra |
+----------------+---------------+------+-----+---------+-------+
| Payment_ID     | int(11)       | NO   | PRI | NULL    |       |
| Booking_ID     | int(11)       | YES  | UNI | NULL    |       |
| Payment_Date   | datetime      | YES  |     | NULL    |       |
| Amount         | decimal(10,2) | YES  |     | NULL    |       |
| Payment_Method | varchar(50)   | YES  |     | NULL    |       |
| Payment_Status | varchar(20)   | YES  |     | NULL    |       |
+----------------+---------------+------+-----+---------+-------+
```

## Query : Insert Values In Airline Table

```sql
INSERT INTO Airline VALUES
    -> (1, 'Air India', '9876543210'),
    -> (2, 'IndiGo', '9123456780');
    SELECT * FROM Airline;
```

## Output :

```sql
+------------+--------------+----------------+
| Airline_ID | Airline_Name | Contact_Number |
+------------+--------------+----------------+
|          1 | Air India    | 9876543210     |
|          2 | IndiGo       | 9123456780     |
+------------+--------------+----------------+
```

## Query : Insert Values In Airport Table

```sql
INSERT INTO Airport VALUES
    -> (101, 'Indira Gandhi International Airport', 'Delhi', 'India'),
    -> (102, 'Chhatrapati Shivaji Maharaj International Airport', 'Mumbai', 'India'),
    -> (103, 'Kempegowda International Airport', 'Bangalore', 'India');
     SELECT * FROM AIRPORT;
```

## Output :

```sql
+------------+---------------------------------------------------+-----------+---------+
| Airport_ID | Airport_Name                                      | City      | Country |
+------------+---------------------------------------------------+-----------+---------+
|        101 | Indira Gandhi International Airport               | Delhi     | India   |
|        102 | Chhatrapati Shivaji Maharaj International Airport | Mumbai    | India   |
|        103 | Kempegowda International Airport                  | Bangalore | India   |
```

## Query : Insert Values In Aircraft Table

```sql
INSERT INTO Aircraft VALUES
    -> (201, 'Boeing 787', 250, 1),
    -> (202, 'Airbus A320', 180, 2),
    -> (203, 'Boeing 737', 200, 1);
    SELECT * FROM AIRCRAFT;
```

## Output :

```sql
+-------------+-------------+-------------+------------+
| Aircraft_ID | Model       | Total_Seats | Airline_ID |
+-------------+-------------+-------------+------------+
|         201 | Boeing 787  |         250 |          1 |
|         202 | Airbus A320 |         180 |          2 |
|         203 | Boeing 737  |         200 |          1 |
+-------------+-------------+-------------+------------+
```

## Query : Insert Values In Flight Table

```sql
INSERT INTO Flight VALUES
    -> (301, 'AI101', 1, 101, 102, '2026-03-01 08:00:00', '2026-03-01 10:00:00', 201),
    -> (302, '6E202', 2, 102, 103, '2026-03-02 14:00:00', '2026-03-02 16:00:00', 202),
    -> (303, 'AI202', 1, 103, 101, '2026-03-03 09:00:00', '2026-03-03 11:30:00', 201),
    -> (304, '6E303', 2, 101, 103, '2026-03-04 15:00:00', '2026-03-04 17:00:00', 202);
    SELECT * FROM FLIGHT;
```

## Output :

```sql
+-----------+---------------+------------+-------------------+------------------------+---------------------+---------------------+-------------+
| Flight_ID | Flight_Number | Airline_ID | Source_Airport_ID | Destination_Airport_ID | Departure_Time      | Arrival_Time        | Aircraft_ID |
+-----------+---------------+------------+-------------------+------------------------+---------------------+---------------------+-------------+
|       301 | AI101         |          1 |               101 |                    102 | 2026-03-01 08:00:00 | 2026-03-01 10:00:00 |         201 |
|       302 | 6E202         |          2 |               102 |                    103 | 2026-03-02 14:00:00 | 2026-03-02 16:00:00 |         202 |
|       303 | AI202         |          1 |               103 |                    101 | 2026-03-03 09:00:00 | 2026-03-03 11:30:00 |         201 |
|       304 | 6E303         |          2 |               101 |                    103 | 2026-03-04 15:00:00 | 2026-03-04 17:00:00 |         202 |
+-----------+---------------+------------+-------------------+------------------------+---------------------+---------------------+-------------+
```

## Query : Insert Values In Passenger Table

```sql
 INSERT INTO Passenger VALUES
    -> (401, 'Rahul Sharma', 'Male', '1995-06-15', '9000000001', 'rahul@gmail.com', 'P1234567'),
    -> (402, 'Priya Verma', 'Female', '1998-09-20', '9000000002', 'priya@gmail.com', 'P7654321'),
    -> (403, 'Amit Kumar', 'Male', '1992-03-10', '9000000003', 'amit@gmail.com', 'P1112223'),
    -> (404, 'Sneha Reddy', 'Female', '1997-11-05', '9000000004', 'sneha@gmail.com', 'P4445556'),
    -> (405, 'Arjun Mehta', 'Male', '1988-07-22', '9000000005', 'arjun@gmail.com', 'P7778889'),
    -> (406, 'Neha Singh', 'Female', '1993-01-18', '9000000006', 'neha@gmail.com', 'P9990001');
    SELECT * FROM PASSENGER;
```

## Output :

```sql
+--------------+--------------+--------+---------------+------------+-----------------+-------------+
| Passenger_ID | Name         | Gender | Date_of_Birth | Phone      | Email           | Passport_No |
+--------------+--------------+--------+---------------+------------+-----------------+-------------+
|          401 | Rahul Sharma | Male   | 1995-06-15    | 9000000001 | rahul@gmail.com | P1234567    |
|          402 | Priya Verma  | Female | 1998-09-20    | 9000000002 | priya@gmail.com | P7654321    |
|          403 | Amit Kumar   | Male   | 1992-03-10    | 9000000003 | amit@gmail.com  | P1112223    |
|          404 | Sneha Reddy  | Female | 1997-11-05    | 9000000004 | sneha@gmail.com | P4445556    |
|          405 | Arjun Mehta  | Male   | 1988-07-22    | 9000000005 | arjun@gmail.com | P7778889    |
|          406 | Neha Singh   | Female | 1993-01-18    | 9000000006 | neha@gmail.com  | P9990001    |
+--------------+--------------+--------+---------------+------------+-----------------+-------------+
```

## Query : Insert Values In Booking Table

```sql
INSERT INTO Booking VALUES
    -> (501, 401, 301, '2026-02-25 12:30:00', '12A', 'Economy', 'Confirmed'),
    -> (502, 402, 302, '2026-02-26 09:15:00', '5C', 'Business', 'Confirmed'),
    -> (503, 403, 301, '2026-02-27 10:00:00', '14B', 'Economy', 'Confirmed'),
    -> (504, 404, 302, '2026-02-27 11:15:00', '6A', 'Business', 'Confirmed'),
    -> (505, 405, 303, '2026-02-28 09:30:00', '10C', 'Economy', 'Cancelled'),
    -> (506, 406, 304, '2026-02-28 14:45:00', '8D', 'Economy', 'Confirmed');
    SELECT * FROM BOOKING;
```

## Output :

```sql
+------------+--------------+-----------+---------------------+-------------+----------+-----------+
| Booking_ID | Passenger_ID | Flight_ID | Booking_Date        | Seat_Number | Class    | Status    |
+------------+--------------+-----------+---------------------+-------------+----------+-----------+
|        501 |          401 |       301 | 2026-02-25 12:30:00 | 12A         | Economy  | Confirmed |
|        502 |          402 |       302 | 2026-02-26 09:15:00 | 5C          | Business | Confirmed |
|        503 |          403 |       301 | 2026-02-27 10:00:00 | 14B         | Economy  | Confirmed |
|        504 |          404 |       302 | 2026-02-27 11:15:00 | 6A          | Business | Confirmed |
|        505 |          405 |       303 | 2026-02-28 09:30:00 | 10C         | Economy  | Cancelled |
|        506 |          406 |       304 | 2026-02-28 14:45:00 | 8D          | Economy  | Confirmed |
+------------+--------------+-----------+---------------------+-------------+----------+-----------+
```

## Query : Insert Values In Payment Table

```sql
INSERT INTO Payment VALUES
    -> (601, 501, '2026-02-25 12:45:00', 7500.00, 'Credit Card', 'Successful'),
    -> (602, 502, '2026-02-26 09:30:00', 9500.00, 'UPI', 'Successful'),
    -> (603, 503, '2026-02-27 10:10:00', 7600.00, 'Debit Card', 'Successful'),
    -> (604, 504, '2026-02-27 11:20:00', 9800.00, 'Credit Card', 'Successful'),
    -> (605, 505, '2026-02-28 09:45:00', 8200.00, 'Net Banking', 'Refunded'),
    -> (606, 506, '2026-02-28 15:00:00', 7900.00, 'UPI', 'Successful');
    SELECT * FROM PAYMENT;
```

## Output :

```sql
SELECT * FROM PAYMENT;
+------------+------------+---------------------+---------+----------------+----------------+
| Payment_ID | Booking_ID | Payment_Date        | Amount  | Payment_Method | Payment_Status |
+------------+------------+---------------------+---------+----------------+----------------+
|        601 |        501 | 2026-02-25 12:45:00 | 7500.00 | Credit Card    | Successful     |
|        602 |        502 | 2026-02-26 09:30:00 | 9500.00 | UPI            | Successful     |
|        603 |        503 | 2026-02-27 10:10:00 | 7600.00 | Debit Card     | Successful     |
|        604 |        504 | 2026-02-27 11:20:00 | 9800.00 | Credit Card    | Successful     |
|        605 |        505 | 2026-02-28 09:45:00 | 8200.00 | Net Banking    | Refunded       |
|        606 |        506 | 2026-02-28 15:00:00 | 7900.00 | UPI            | Successful     |
+------------+------------+---------------------+---------+----------------+----------------+
```

## Query : Show bookings of a particular passenger

```sql
SELECT * FROM Booking WHERE Passenger_ID = 401;
```

## Output :

```sql
+------------+--------------+-----------+---------------------+-------------+---------+-----------+
| Booking_ID | Passenger_ID | Flight_ID | Booking_Date        | Seat_Number | Class   | Status    |
+------------+--------------+-----------+---------------------+-------------+---------+-----------+
|        501 |          401 |       301 | 2026-02-25 12:30:00 | 12A         | Economy | Confirmed |
+------------+--------------+-----------+---------------------+-------------+---------+-----------+
```

## Query : Show flight details with airline name

```sql
SELECT F.Flight_Number, A.Airline_Name, F.Departure_Time, F.Arrival_Time
    -> FROM Flight F JOIN Airline A ON F.Airline_ID = A.Airline_ID;
```

## Output :

```sql
+---------------+--------------+---------------------+---------------------+
| Flight_Number | Airline_Name | Departure_Time      | Arrival_Time        |
+---------------+--------------+---------------------+---------------------+
| AI101         | Air India    | 2026-03-01 08:00:00 | 2026-03-01 10:00:00 |
| 6E202         | IndiGo       | 2026-03-02 14:00:00 | 2026-03-02 16:00:00 |
| AI202         | Air India    | 2026-03-03 09:00:00 | 2026-03-03 11:30:00 |
| 6E303         | IndiGo       | 2026-03-04 15:00:00 | 2026-03-04 17:00:00 |
+---------------+--------------+---------------------+---------------------+
```

## Query : Show passenger name with their booked flight number

```sql
SELECT P.Name, F.Flight_Number FROM Booking B
    -> JOIN Passenger P ON B.Passenger_ID = P.Passenger_ID
    -> JOIN Flight F ON B.Flight_ID = F.Flight_ID;
```

## Output :

```sql
+--------------+---------------+
| Name         | Flight_Number |
+--------------+---------------+
| Rahul Sharma | AI101         |
| Amit Kumar   | AI101         |
| Priya Verma  | 6E202         |
| Sneha Reddy  | 6E202         |
| Arjun Mehta  | AI202         |
| Neha Singh   | 6E303         |
+--------------+---------------+
```

## Query : Show all payments with booking details

```sql
SELECT P.Payment_ID, P.Amount, B.Booking_ID, B.Status FROM Payment P
    -> JOIN Booking B ON P.Booking_ID = B.Booking_ID;
```

## Output :

```sql
+------------+---------+------------+-----------+
| Payment_ID | Amount  | Booking_ID | Status    |
+------------+---------+------------+-----------+
|        601 | 7500.00 |        501 | Confirmed |
|        602 | 9500.00 |        502 | Confirmed |
|        603 | 7600.00 |        503 | Confirmed |
|        604 | 9800.00 |        504 | Confirmed |
|        605 | 8200.00 |        505 | Cancelled |
|        606 | 7900.00 |        506 | Confirmed |
+------------+---------+------------+-----------+
```

## Query : Find all flights from a specific airport

```sql
SELECT * FROM Flight WHERE Source_Airport_ID = 102;
```

## Output :

```sql
+-----------+---------------+------------+-------------------+------------------------+---------------------+---------------------+-------------+
| Flight_ID | Flight_Number | Airline_ID | Source_Airport_ID | Destination_Airport_ID | Departure_Time      | Arrival_Time        | Aircraft_ID |
+-----------+---------------+------------+-------------------+------------------------+---------------------+---------------------+-------------+
|       302 | 6E202         |          2 |               102 |                    103 | 2026-03-02 14:00:00 | 2026-03-02 16:00:00 |         202 |
+-----------+---------------+------------+-------------------+------------------------+---------------------+---------------------+-------------+
```

## Query : Show confirmed bookings only

```sql
SELECT * FROM Booking WHERE Status = 'Confirmed';
```

## Output :

```sql
+------------+--------------+-----------+---------------------+-------------+----------+-----------+
| Booking_ID | Passenger_ID | Flight_ID | Booking_Date        | Seat_Number | Class    | Status    |
+------------+--------------+-----------+---------------------+-------------+----------+-----------+
|        501 |          401 |       301 | 2026-02-25 12:30:00 | 12A         | Economy  | Confirmed |
|        502 |          402 |       302 | 2026-02-26 09:15:00 | 5C          | Business | Confirmed |
|        503 |          403 |       301 | 2026-02-27 10:00:00 | 14B         | Economy  | Confirmed |
|        504 |          404 |       302 | 2026-02-27 11:15:00 | 6A          | Business | Confirmed |
|        506 |          406 |       304 | 2026-02-28 14:45:00 | 8D          | Economy  | Confirmed |
+------------+--------------+-----------+---------------------+-------------+----------+-----------+
```

## Query : Show total revenue (sum of payments)

```sql
SELECT SUM(Amount) AS Total_Revenue FROM Payment;
```

## Output :

```sql
+---------------+
| Total_Revenue |
+---------------+
|      50500.00 |
+---------------+
```

## Query : Find the passenger who paid the highest amount

```sql
SELECT P.Name, PM.Amount FROM Payment PM
    -> JOIN Booking B ON PM.Booking_ID = B.Booking_ID
    -> JOIN Passenger P ON B.Passenger_ID = P.Passenger_ID
    -> WHERE PM.Amount = (SELECT MAX(Amount) FROM Payment);
```

## Output :

```sql
+-------------+---------+
| Name        | Amount  |
+-------------+---------+
| Sneha Reddy | 9800.00 |
+-------------+---------+
```

## Query : Find flights operating between two specific cities

```sql
SELECT F.Flight_Number FROM Flight F
    -> JOIN Airport A1 ON F.Source_Airport_ID = A1.Airport_ID
    -> JOIN Airport A2 ON F.Destination_Airport_ID = A2.Airport_ID
    -> WHERE A1.City = 'Delhi' AND A2.City = 'Mumbai';
```

## Output :

```sql
+---------------+
| Flight_Number |
+---------------+
| AI101         |
+---------------+
```
