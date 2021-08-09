# TrackService
The project I would like to develop is an App named TrackService. It provides a database for the vehicle owner and the owner of the auto service to search car service records, updates new service records include air filter change, extensive brake inspection, etc. At the same time, brand information on the part and the date of the next estimated service would be automatically updated.



## Structural Database Rules

1. Each service history is associated with a car; each car may be associated with many service histories.
2. Each service history is made from an auto shop. Each auto shop has zero to many service histories.

3. Each service history has one or more product information; each product information is associated with one to many service histories. 

4. Each customer may have zero to many cars. Each car has exactly one owner. 

   ![](/clip_image002.png)

## Conceptual entity-relationship diagram

1. An account is a free account or a paid account.

2. A car is Ferrari, Aston martin, Honda Accord or etc.

3. An auto shop could be auto care center, tire center and brake center, both, and none of these.

4. The service history is steering alignment, filter change, oil change, battery change, both, and none of these. 

5. The production information is battery, tire, or none of these.

![img](img/clip_image003.png)

## Attributes

| Table                   | Attribute            | Data  type     | Reasoning                                                    |
| ----------------------- | -------------------- | -------------- | ------------------------------------------------------------ |
| Customer                | ACCOUNT_NUMBER       | Decimal  (12)  | Every  Customer should has a unique account number to identify their identity. |
| Customer                | Last_name            | Varchar  (255) | This  is the last name of the account holder, up to 255 characters of the last  name. |
| Customer                | First_name           | Varchar  (255) | This  is the first name of the account holder, up to 255 characters of the first  name |
| Customer                | Date_of_birth        | Date           | This  is the date of birth of account holder, it is used to identify the identity  of account holder. |
| Customer                | Encrypted  Password  | Varchar  (255) | Every  Account has a password. It would be stored in encrypted text format in the  database. Varchar 255 ensure the security of the account. |
| Car_information         | VIN_Number           | Varchar  (64)  | Every  car has its own VIN number, this number is different with other car in the  world. |
| Car_information         | Make_of_Car          | Varchar  (255) | This  is the make of the car. Varchar 255 should be upper bound. |
| Car_information         | Model_of_Car         | Varchar  (255) | Varchar  255 in case there is a long model name. It should be upper bound. |
| Car_information         | Year_of_Car          | Decimal  (12)  | This  is the year of car. Decimal 12 should be upper bound.  |
| Auto  Shop Owner        | Autoshop_id          | Varchar  (12)  | Every  auto shop owner could use this unique.                |
| Auto  Shop Owner        | Last_name            | Varchar  (64)  | This  is the last name of the auto shop owner.               |
| Auto  Shop Owner        | First_name           | Varchar  (64)  | This  is the first name of the auto shop owner.              |
| Auto  Shop Owner        | Business_Field       | Varchar  (255) | The  auto shop owner could write the description about their auto shop so that the  customer could know what kind of service they have. I allow varchar (255) to  ensure they can write everything they want in the description. |
| Auto  Shop Owner        | Date_of_Birth        | DATE           | It  is the date of birth of auto shop owner. It used to identify the identity of  auto shop owner. |
| Production  information | Product_id           | Decimal  (12)  | Different  product has its unique product id. Decimal (12) allow a series of number to  identity different products. |
| Production  information | Name_of_part         | Varchar  (255) | Every  part of car has its unique name. Varchar (255) should be a safe upper bound. |
| Production  information | Producer_of_part     | Varchar  (255) | The  is the producer of the part of car. Varchar 255 should be a safe upper bound. |
| Production  information | Date_of_produce      | Date           | This  is the data of producing.                              |
| Service  History        | Service_Number       | Decimal  (12)  | I  used decimal (12) to create a series of number to identify different case of  service. |
| Service  History        | Date_of_Service      | Date           | It  is used to record the date of service.                   |
| Service  History        | Mile_number          | Decimal  (12)  | Every  car has its mile record, I use decimal 12 in case.    |
| Service  History        | Date_of_next_service | Date           | It  is used to mention the owner of car when is next service. |
| Producer_Information    | Producer_id          | Decimal  (12)  | Decimal  should be the upper bound here.                     |
| Type  of Product        | Type_id              | Decimal  (12)  | Decimal  should be the upper bound here.                     |

## DBMS Physical ERD

There are two additional entities after normalization. They are producer information and product types. In producer information entities, producer id is the primary key here and is a foreign key in product information so that it could avoid redundancy in the future using. At the same time, there are different types of vehicle parts in the market. In product types, different primary key symbolizes different types of product

According to these two new entities, there are two new database rules that used to reflect these entities. 

1. Each product is manufactured by a company. Each company could manufactured many products.
2. The production information is battery, tire, or none of these.

The producer information and product types are now include in the conceptual ERD, and conceptual ERD is in sync with the structural database rules and the DBMS physical ERD.

![Screen Shot 2020-11-12 at 7.39.44 PM](/clip_image004.png)

## Create Script

In this part, I first drop all tables which might have the same name and it is a script that could be execute multiple times. The screens shot contain the scripts which include attributes and constraints. Note that, I run this script under SQL developer. 

![img](/clip_image006.png)

![Screen Shot 2020-11-12 at 7.54.19 PM](/clip_image007.png)

The columns and constraints are executed according to physical ERD and conceptual ERD provide before.

## Index Creation

Here is a screen shot about the script of creating index for database. I create some non-unique and unique index in this application database system.

![Screen Shot 2020-11-12 at 7.11.44 PM](/clip_image008.png)

To have high efficiency in the daily use, I create ProducerIdIdx, TypeIDIdx, AutoshopIdIdx, VinNumberIdx, and AccountIdx to retrieve the information quickly. 



## Application Transaction

Add Vehicle Use Case 

1. Andy is a customer of this application. 

2. He purchases a new vehicle from dealer, and he want to add his vehicle to his account.

3. He login his account and click add vehicle and enter the information about his vehicle into system. 

 

In this Use Case, I would like to create procedure help us to finish. This procedure is named Add Vehicle. In this procedure, it would takes vin number of vehicles, make of car, model of car, year of car and mileage of car. 

 

This is my screenshot of my stored procedure definition. 

![img](/clip_image009.png)

Andy’s account id is 874419890. The vin number of this vehicle is 1HGBH41JXMN102345. The make of this vehicle is BMW and model is X5 and year of vehicle is 2015. Since some of information is primary key in other tables, it is necessary to check the unique of this information. 

 

Here is a screenshot of my stored procedure executions. 

![img](/clip_image0010.png)

![img](/clip_image0011.png)

![img](/clip_image0012.png)

After executing this procedure with this information, we can find this record in the database clearly. Here is the screenshot about the database of car information in his account. 



## DBMS Physical ERD with Service History change.

After reviewing my DBMS and conceptual ERD, it is useful to check the service history of the vehicle in the database. However, it is necessary to create a procedure that add the mileage history change in the database. So, here are some new database rules: Each vehicle could have many zero or many mileage changes; each mileage change is for a unique vehicle. One mileage change record associate with one service history change. One mileage change associate with one service history. 

Here is the update conceptual ERD below. 

![img](/clip_image0013.png)

I added the service history change entity into conceptual ERD. Here are attributes of this entity in the DBMS physical ERD. 

| **Attributes**  | **Description**                                              |
| --------------- | ------------------------------------------------------------ |
| MileageChangeID | This  is the primary key of this history table. It is a DECIMAL (12) allow for many  values. |
| ChangeDate      | This  is the date the mileage update, with DATE datatype.    |
| PreviousMileage | This  the old number of mileage. It is a DECIMAL (12) allow for many values. |
| NewMileage      | This  the new number of mileage. Decimal (12) allow for many values. |
| VINNUMBER       | This  is the foreign key of this history table. It is varchar (255) allow for many  values. |

 

Here is a screenshot of table creating. All attributes are the same with the attributes in DBMS physical ERD. 

![img](/clip_image0014.png)

Here is a screenshot of my trigger creation which will maintain the HistoryChange table.

![img](/clip_image0015.png)

I explain it line by line. 

![img](/clip_image0016.png)

| **create or replace   TRIGGER MileageChange  BEFORE UPDATE OF Mileage ON  CARINFORMATION** | **This  starts the definition of trigger and names it “MileageChange”. The trigger is  linked to the Carinformation table and is executed automatically after any updated  about mileage to that table.** |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| **FOR EACH ROW  BEGIN**                                      | **This  is part of syntax starting the trigger block.**      |
| **INSERT INTO  mileagechange(mileagechangeid, vin_number, PREVIOUSMILEAGE, NEWMILEAGE,  CHANGEDATE)   VALUES(NVL((SELECT MAX(MILEAGECHANGEID)+1  FROM mileagechange), 1),   :OLD.vin_number,   :OLD.MILEAGE,   :New.MILEAGE,   trunc(sysdate));** | **This  insert the record into mileagechange table with require information. The  primary key here is mileagechangeid. It could be automatically generated by  nvl function and get a maximal number in the table. For other information  like vin number and mileage, they could be obtain by old and new information.** |
| **END;**                                                     | **This  ends the trigger definition**                        |

 

![img](/clip_image0017.png)

![img](/clip_image018.png) 

 

After update four times mileage record, it is necessary to check the mileagechange table. 

![img](/clip_image019.png)

Now, it is clear to see the vehicle which vin number is 1HGBH41JXMN109186 has four records about mileage change. Since the mileage change record is reported by service, it is clear to count the number of services the owner have in the database.

 

## Question and Query

It is interesting to figure out how many paid accounts has two and more vehicles. Compare with free account, the advantage of paid account can register more than two vehicles in the application. As the developer of application, it is useful to know how many paid accounts customer register two and more than two vehicle in the application.

 

Firstly, I need to make a list of car that belong to paid account so that I can continue to calculate the number of paid account who has two and more than two vehicle in their account. 

Here is a screenshot of the query I use. 

![img](/clip_image020.png) ![img](/clip_image021.png)

To show this function work correctly, this is all information that stored in the database.

![img](/clip_image022.png)

![img](/clip_image023.png)

 

Then, it is useful to find the customer who has service records at the auto shop owner whose business field is oil change. 

![img](/clip_image024.png)

![img](/clip_image025.png)

![img](/clip_image026.png)

![img](/clip_image027.png)

Here is the information about the different tables. In fact, the main table is service history. It connect with different tables and share different foreign keys.
