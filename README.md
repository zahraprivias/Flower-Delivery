# Flower-Delivery
Quiz for Database course. Demonstrates ability in DDL and DML such as CREATE TABLE, ALTER TABLE, INSERT, UPDATE, SELECT, and CREATE VIEW.

## Table of Contents

## Relational Table
<img src="https://github.com/zahraprivias/Flower-Delivery/blob/main/ERD.PNG" alt="Image" width="490" height="420">  

## Case  
1. Create a table named **DeliveryType** with the following description:  

Field Name | Data Type | Length | Notes  
--- | --- | --- | ---  
DeliveryID | CHAR | 6 | Primary key. DeliveryID  must be started with ‘DLR’ and followed by 3 characters of number. Example: DLR001  
DeliveryTypeName | VARCHAR | 50 | Can’t be empty and DeliveryTypeName must be between ‘Regular’ or ‘Express’  
DeliveryCost | INT | - | Can't be empty.  
2. Add a new column on **Staff** named Salary with int data type. Then delete the column.  
3. Insert the following data into **Staff** table.  
4. Display FlowerID, FlowerName, FlowerColor, FlowerType, and Price for every flower which name start with ‘P’.  
5. Update **AdditionalRequest** for every transaction that occurred on the 6th day into ‘Ribbon’.  
6. Create view named StaffView to display StaffID, StaffName, Gender (obtained from the first letter of StaffGender), and StaffPosition for every Staff whose position is ‘Florist’.  
7. Display FlowerName, Flower Type (obtained from FlowerType in uppercast format), and Price for every flower which was sold without using Card as an additional Request.  
8. Display Customer Name (obtained by adding ‘Mr. ’ in front of CustomerName), Customer Phone (obtained from CustomerPhone), Transaction Date (obtained from TransactionDate in dd MM yyyy format), Transaction Day (obtained from name of the day from TransactionDay), and Transaction Count (obtained from total number of transaction) for every customer that has done a transaction with staff which ID is ‘STF005’ and at branch which ID is ‘BN005’. Then combine it with Customer Name (obtained by adding ‘Ms. ’ in front of CustomerName), Customer Phone (obtained from CustomerPhone), Transaction Date (obtained from TransactionDate in dd MM yyyy format), Transaction Day (obtained from name of the day from TransactionDay), and Transaction Count (obtained from total number of transaction) for every female customer that has done a transaction with staff which ID is ‘STF001’.  
9. Display TransactionID, FlowerName, Transaction Count (obtained from total number of transaction ended with ‘ Times’), and Remaining Date (obtained from day difference between TransactionDate and 1st April 2016) for every transactions which done by staff which ID is ‘STF002’ and was located at branch which ID is ‘BN001’.  
10. Display Branch (obtained from BranchName), Remaining Date (obtained from the day difference between TransactionDate and 1st April 2016), and Delivery Cost (obtained by adding ‘Rp. ’ in front of Price) for every Transaction for every transaction which sold a flower which price is higher than average value of flower price and Branch name starts with ‘L’.  

## Solution
First, import the database Flower Delivery from **create+insert.sql**  

1. Create a table named **DeliveryType**
```sql
CREATE TABLE DeliveryType (
	DeliveryID CHAR(6) PRIMARY KEY CHECK(DeliveryID LIKE 'DLR[0-9][0-9][0-9]'),
	DeliveryTypeName VARCHAR(50) NOT NULL CHECK(DeliveryTypeName LIKE 'Regular' OR DeliveryTypeName LIKE 'Express'),
	DeliveryCost INT NOT NULL
)
```  
2. 
```sql
ALTER TABLE Staff
ADD Salary INT

ALTER TABLE Staff
DROP COLUMN Salary
```  
3. 
```sql
INSERT INTO Staff(StaffID, StaffName, StaffGender, StaffDOB, StaffPosition, StaffEmail, StaffAddress, StaffPhone) VALUES
('STF008', 'Agus Sasmito', 'Male', '1989-12-29', 'Driver', 'ajustgaus@sasa.com', 'Graha Medika Street no 188 Jakarta', '0810178')
```  
4. 
```sql
SELECT FlowerID, FlowerName, FlowerColor, FlowerType, Price
FROM Flower
WHERE FlowerName LIKE 'P%'
```  
Result:  
<img width="256" alt="No 4" src="https://user-images.githubusercontent.com/96785017/187067027-c466e884-b417-4369-969c-87369cdaf954.PNG">  
5. 
```sql
UPDATE DetailTransaction
SET AdditionalReq = 'Ribbon'
FROM DetailTransaction dt, HeaderTransaction ht
WHERE dt.TransactionID = ht.TransactionID AND DAY(TransactionDate) = 6
```  
6. 
```sql
CREATE VIEW StaffView
AS
	SELECT 
	StaffID, 
	StaffName, 
	[Gender] = LEFT(StaffGender, 1), 
	StaffPosition
	FROM Staff
	WHERE StaffPosition = 'Florist'
GO
```  
7. 
```sql
SELECT 
	FlowerName,
	[Flower Type] = UPPER(FlowerType),
	Price
FROM Flower
WHERE FlowerID IN (
	SELECT FlowerID
	FROM DetailTransaction
	WHERE AdditionalReq != 'Card'
)
```
Result:  
<img width="180" alt="No 7" src="https://user-images.githubusercontent.com/96785017/187067254-a41062e9-ca0a-4a9f-821d-49235ded65a1.PNG">  

8. 
```sql
SELECT
	[Customer Name] = 'Mr. ' + CustomerName,
	[Customer Phone] = CustomerPhone,
	[Transaction Date] = CONVERT(VARCHAR, TransactionDate, 106),
	[Transaction Day] = DATENAME(WEEKDAY, TransactionDate),
	[Transaction Count] = COUNT(TransactionID)
FROM Customer c, HeaderTransaction ht
WHERE 
	c.CustomerID = ht.CustomerID AND 
	StaffID = 'STF005' AND BranchID = 'BN005'
GROUP BY CustomerName, CustomerPhone, TransactionDate
UNION
SELECT
	[Customer Name] = 'Ms. ' + CustomerName,
	[Customer Phone] = CustomerPhone,
	[Transaction Date] = CONVERT(VARCHAR, TransactionDate, 106),
	[Transaction Day] = DATENAME(WEEKDAY, TransactionDate),
	[Transaction Count] = COUNT(TransactionID)
FROM Customer c, HeaderTransaction ht
WHERE 
	c.CustomerID = ht.CustomerID AND 
	StaffID = 'STF001' AND CustomerGender = 'Female'
GROUP BY CustomerName, CustomerPhone, TransactionDate
```  
Result:  
<img width="388" alt="No 8" src="https://user-images.githubusercontent.com/96785017/187067284-36a22daa-9762-4560-b2d9-ff43aeb25591.PNG">  

9. 
```sql
SELECT 
	ht.TransactionID,
	f.FlowerName,
	[Transaction Count] = CAST(COUNT(ht.TransactionID) AS VARCHAR) + ' Times',
	[Remaining Date] = DATEDIFF(DAY, '2016/04/01', TransactionDate)
FROM 
	Flower f JOIN DetailTransaction dt ON f.FlowerID = dt.FlowerID JOIN
	HeaderTransaction ht ON dt.TransactionID = ht.TransactionID
WHERE
	StaffID = 'STF002' AND BranchID ='BN001'
GROUP BY ht.TransactionID, f.FlowerName, TransactionDate
```  
Result:  
<img width="279" alt="No 9" src="https://user-images.githubusercontent.com/96785017/187067272-ccc63a72-1c45-43a9-9b35-c42a46db2e59.PNG">  

10. 
```sql
SELECT
	[Branch] = BranchName,
	[Remaining Date] = DATEDIFF(DAY, '2016/04/01', TransactionDate),
	[Delivery Cost] = 'Rp ' + CAST(Price AS VARCHAR)
FROM 
	Branch b JOIN HeaderTransaction ht ON b.BranchID = ht.BranchID JOIN
	DetailTransaction dt ON ht.TransactionID = dt.TransactionID JOIN
	Flower f ON dt.FlowerID = f.FlowerID,(
	SELECT [Avg Price] = AVG(Price)
	FROM Flower
	) AS AvgPrice
WHERE 
	Price > AvgPrice.[Avg Price] AND
	b.BranchName LIKE 'L%'
GROUP BY BranchName, TransactionDate, Price
``` 
Result: 
<img width="184" alt="No 10" src="https://user-images.githubusercontent.com/96785017/187067265-d376d534-eb5e-41fb-9136-64872451f0a5.PNG">
