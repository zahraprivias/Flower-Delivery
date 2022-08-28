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

