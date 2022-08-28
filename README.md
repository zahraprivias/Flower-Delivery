# Flower-Delivery
Quiz for Database course. Demonstrates ability in DDL and DML such as CREATE TABLE, ALTER TABLE, INSERT, UPDATE, SELECT, and CREATE VIEW.

## Table of Contents

## Case
<img src="https://github.com/zahraprivias/Flower-Delivery/blob/main/ERD.PNG" alt="Image" width="490" height="420">  
1. Create a table named **DeliveryType** with the following description:  
Field Name | Data Type | Length | Notes  
--- | --- | --- | ---  
DeliveryID | CHAR | 6 | Primary key. DeliveryID  must be started with ‘DLR’ and followed by 3 characters of number. Example: DLR001  
DeliveryTypeName | VARCHAR | 50 | Can’t be empty and DeliveryTypeName must be between ‘Regular’ or ‘Express’  
DeliveryCost | INT | - | Can't be empty.

