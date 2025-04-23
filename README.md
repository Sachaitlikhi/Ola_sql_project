# Ola_sql_project

![Ola Logo](https://github.com/Sachaitlikhi/Ola_sql_project/blob/main/images.png)


## 📊 Overview

This project involves an in-depth analysis of Ola's ride data for the month of July. The goal is to generate insights that can help improve customer satisfaction, optimize ride services, and make data-driven decisions regarding vehicle types, ride statuses, customer ratings, and payment methods. This README outlines the objectives, business problems, solutions, and key findings from the analysis.

---

## 🎯 Objectives

- **Successful Bookings**: Identify and analyze all successful bookings.
- **Vehicle Performance**: Measure the average ride distance by vehicle type and identify top-performing vehicles.
- **Canceled Rides**: Investigate the reasons behind ride cancellations, including customer-initiated and driver-initiated cancellations.
- **Customer Insights**: Identify the top customers who booked the most rides and analyze their behavior.
- **Payment Methods**: Explore payment methods used by customers, with a focus on UPI transactions.
- **Rating Analysis**: Assess the average ratings given by customers for each vehicle type and the highest and lowest driver ratings for specific vehicle types.
- **Incomplete Rides**: Investigate the reasons for incomplete rides and their impact on service.

---

## 🗃️ Dataset

- **Source:** Internal Ola Data (July 2023)

---

## 🧱 Schema

```sql
DROP TABLE IF EXISTS July_data;
CREATE TABLE July_data
(
    Booking_ID               INT,
    Customer_ID              INT,
    Vehicle_Type             VARCHAR(50),
    Ride_Distance            FLOAT,
    Booking_Status           VARCHAR(20),
    Driver_Ratings           FLOAT,
    Customer_Rating          FLOAT,
    Payment_Method           VARCHAR(20),
    Booking_Value            FLOAT,
    Incomplete_Rides         VARCHAR(5),
    Incomplete_Rides_Reason  VARCHAR(255),
    Canceled_Rides_by_Driver VARCHAR(255)
);
```



### 1. Retrieve all successful bookings

```sql
SELECT * FROM [Ola].[dbo].[July_data]
  WHERE Booking_Status = 'Success';
```

**Objective:** Get a complete list of all successful bookings in July.


### 2. Find the average ride distance for each vehicle type

```sql
SELECT Vehicle_Type , AVG(Ride_Distance) AS AVG_DISTANCE
FROM [Ola].[dbo].[July_data]
GROUP BY Vehicle_Type 
```

**Objective:** Determine the average ride distance for each type of vehicle in the dataset.



### 3. Get the total number of cancelled rides by customers

```sql
SELECT COUNT(*) AS COUNT_OF_CANCLLED_RIDES_BY_CUSTOMER 
FROM [Ola].[dbo].[July_data]
WHERE Booking_Status = 'Canceled by Customer';
```

**Objective:**  Calculate the total number of rides canceled by customers.

### 4. List the top 5 customers who booked the highest number of rides

```sql
 SELECT TOP 5 Customer_ID, COUNT(Booking_ID) as total_count_of_bookings
FROM [Ola].[dbo].[July_data]
GROUP BY Customer_ID
ORDER BY count(Booking_ID) DESC;
```

**Objective:** Identify the top 5 customers who booked the most rides during July.

### 5. Get the number of rides cancelled by drivers due to personal and car-related issues

```sql
SELECT COUNT(*) as total_rides_cancelled_by_driver_PCI
FROM [Ola].[dbo].[July_data]
WHERE Canceled_Rides_by_Driver = 'Personal & Car related issue'
```

**Objective:** Determine how many rides were canceled by drivers due to personal and car-related issues.

### 6. Find the maximum and minimum driver ratings for Prime Sedan bookings

```sql
SELECT MAX(Driver_Ratings) AS MAX_RATINGS
, MIN(Driver_Ratings) AS MINIMUM_RATINGS
FROM [Ola].[dbo].[July_data]
WHERE Vehicle_Type = 'Prime Sedan';
```

**Objective:** Identify the highest and lowest driver ratings for Prime Sedan bookings.

### 7. Retrieve all rides where payment was made using UPI

```sql
SELECT * FROM [Ola].[dbo].[July_data]
WHERE Payment_Method = 'UPI';'
```

**Objective:** Get all rides where the payment was made using UPI.


### 8. Find the average customer rating per vehicle type

```sql
SELECT Vehicle_Type, AVG(Customer_Rating) AVG_CUSTOMER_RATING
FROM [Ola].[dbo].[July_data]
GROUP BY Vehicle_Type;
```

**Objective:** Calculate the average customer rating for each vehicle type.

### 9. Calculate the total booking value of rides completed successfully

```sql
SELECT SUM(Booking_Value)
FROM [Ola].[dbo].[July_data]
WHERE Booking_Status = 'Success';

```

**Objective:** Determine the total value of successfully completed bookings in July.

### 10. List all incomplete rides along with the reason

```sql
SELECT Booking_ID, Incomplete_Rides_Reason
FROM [Ola].[dbo].[July_data]
WHERE Incomplete_Rides = 'Yes';
```

## Findings and Conclusion

The analysis of Ola's ride data reveals several key insights about customer behavior, driver performance, and ride cancellations. It highlights areas for improvement, such as reducing ride cancellations, optimizing vehicle usage based on ride distance, and providing better insights into customer preferences and payment methods.
