----1. Create database called Brunch
create database Brunch
use Brunch;


---2.Create the primary key tables which they should be called Supermarkets, Ingridients, Dishes, BrunchPlaces and start to add values into it.

create table Supermarkets
(ID INT AUTO_INCREMENT 
primary key NOT NULL,
Name varchar(100))
;
INSERT INTO Supermarkets
(ID, NAME)
VALUES
(1, 'Tesco'),
(2, 'Morrison'),
(3, 'Sainsbury')
;

create table Ingridients
(ID INT AUTO_INCREMENT 
primary key NOT NULL,
Name varchar(100))
;
INSERT INTO Ingridients
(Name)
VALUES
('Flour'),
('Egg'),
('Oil'),
('lemon'),
('Caster Sugar'),
('Bacon'),
('Mushroom'),
('Cherry Tomatoe'),
('Bread'),
('Pork Sausage'),
('Cider vinegar'),
('English Muffins'),
('White Wine Vinegar'),
('Smoked Salmon'),
('Shallot Onion'),
('Dill'),
('Unsalted Butter'),
('White Miso Paste'),
('Double Cream'),
('Avocado'),
('Feta Cheese')
;

Create Table Dishes
(ID INT AUTO_INCREMENT 
primary key NOT NULL,
Name varchar(100))
;
ALTER TABLE Dishes 
ADD (Prep_time varchar(100),
	Cooking_time VARCHAR(100) )
; 
SELECT * FROM
Dishes;

INSERT INTO Dishes
(Name, Prep_time, Cooking_time)
VALUES
('Pancakes',10,20),
('Full English Breakfast', 5, 20),
('Egg Royale', 30, 45),
('Avocado on Toast', 5, 5)
;


Create Table BrunchPlaces
(ID INT AUTO_INCREMENT 
primary key NOT NULL,
Name varchar(100))
;
INSERT INTO BrunchPlaces
(Name)
VALUES
('The Astro Cafe'),
('Cafe 338'),
('The Moonlight Cafe')
;

---3. Create the connection between tables (most of the tables have many to many relationship for example: the same brand of eggs it sold at  3 of the supermarkets. Therefore to maintain a min of 3NF, i need to put a table in between to create two one to many relationships.
Ingridients, Dishes, BrunchPlaces, Supermarket  called them Supermarket_Ingredients table, Dishes_BrunchPlaces table, Dishes_Ingredients

CREATE TABLE Dish_BrunchPlaces 
(ID INT AUTO_INCREMENT 
primary key NOT NULL,
Dish_ID INT, FOREIGN KEY (Dish_ID) REFERENCES Dishes(ID),
BrunchPlace_ID INT, FOREIGN KEY (BrunchPlace_ID) REFERENCES BrunchPlaces(ID),
Price FLOAT)
;

INSERT INTO Dish_BrunchPlaces
(Dish_ID, BrunchPlace_ID, Price)
VALUES
(1, 1, 12.95),
(2, 1, 13.95),
(3, 1, 12.50),
(4, 1, 11.50),
(1, 2, 10.5),
(2, 2, 9.8),
(3, 2, 8.9),
(4, 2, 8.5),
(1, 3, 9.9),
(2, 3, 12.5),
(3, 3, 9.5),
(4, 3, 9.2)
;

SELECT*FROM Dish_BrunchPlaces;

SELECT 
D.name as NameOfDish,
BP.name as NameOfRestaurant,
price
FROM Dish_BrunchPlaces as DBP
LEFT JOIN Dishes as D ON DBP.Dish_ID = D.ID
LEFT JOIN BrunchPlaces as BP ON DBP.BrunchPlace_ID = BP.ID;



CREATE TABLE Dish_Ingridients 
(ID INT AUTO_INCREMENT 
primary key NOT NULL,
Dish_ID INT, FOREIGN KEY (Dish_ID) REFERENCES Dishes(ID),
Ingridient_ID INT, FOREIGN KEY (Ingridient_ID) REFERENCES Ingridients(ID),
Quantity VARCHAR(100))
;

INSERT INTO Dish_Ingridients
(Dish_ID, Ingridient_ID, Quantity)
VALUES
(1,	1,	'100gr'),
(1,	2,	'2 eggs'),
(1,	3,	'1 table spoon oil'),
(1,	4, 'lemon wedges'),
(1,	5,	'14 gr caster sugar'),
(2,	6,	'4 bacon'),
(2,	7,	'4  mushrooms'),
(2,	8,	'12 cherry tomatoes'),
(2,	3,	'6 table spoon oil'),
(2,	9,	'2 slice bread'), 
(2,	10,	'2 pork sausages'),
(2,	2,	'2 eggs'),
(2,	11,	'few drops cider vinegar'),
(3,	12,	'2 English muffins'),
(3,	13,	'7.9ml white wine vinegar'), 
(3,	2,	'4 eggs'),
(3,	14,	'200g smoked salmon'),
(3,	13,	'100ml white wine vinegar'),
(3,	15,	'1 shallot onion'),
(3,	16,	'3 dill sprigs'),
(3,	17,	'125g unsalted butter'),
(3,	2,	'2 egg yolks'),
(3,	18,	'14ml white miso paste'),
(3,	19,	'14 mg double cream'),
(3,	4,	'28ml lemon juice'),
(4,	13,	'28ml white vineger'),
(4,	2,	'2 eggs'),
(4,	20,	'1 avocado'),
(4,	21,	'50g feta'),
(4,	4,	'half lemon juice'),
(4,	9,	'2 slices of sourdough') 
;

SELECT*FROM Dish_Ingridients;

SELECT 
D.name as NameOfDish,
I.name as Ingridient,
Quantity
FROM Dish_Ingridients as DI
LEFT JOIN Dishes as D ON DI.Dish_ID = D.ID
LEFT JOIN Ingridients as I ON DI.Ingridient_ID = I.ID
;

Select * from Dishes where name='Pancakes';

CREATE TABLE Supermarket_Ingridients 
(ID INT AUTO_INCREMENT 
primary key NOT NULL,
Ingridient_ID INT, FOREIGN KEY (Ingridient_ID) REFERENCES Ingridients(ID),
Supermarket_ID INT, FOREIGN KEY (Supermarket_ID) REFERENCES Supermarkets(ID),
SM_Price Float)
;

INSERT INTO Supermarket_Ingridients
(Ingridient_ID, Supermarket_ID, SM_Price)
VALUES
(1,	1, 0.02),
(2,	1, 0.76),
(3, 1, 0.02),
(4, 1, 0.15),
(5, 1, 0.01),
(6, 1, 0.90),
(7,	1, 0.65),
(8,	1, 0.80),
(9,	1, 0.20),
(10,	1, 0.60),
(11,	1, 0.01),
(12,	1, 0.50),
(13,	1, 0.03),
(14,	1, 7),
(15,	1, 0.09),
(16,	1, 0.50),
(17,	1, 1.30),
(18,	1, 0.30),
(19,	1, 0.06),
(20,	1, 0.89),
(21,	1, 0.25),
(1, 2, 0.29),
(2,	2, 0.93),
(3,	2, 0.02),
(4,	2, 0.13),
(5,	2, 0.02),
(6,	2, 0.90),
(7,	2, 0.45),
(8,	2, 0.65),
(9,	2, 0.20),
(10,	2, 0.37),
(11,	2, 0.01),
(12,	2, 0.50),
(13,	2, 0.03),
(14,	2, 5.90),
(15,	2, 0.10),
(16,	2, 0.22),
(17,	2, 1.06),
(18,	2, 0.24),
(19,	2, 0.06),
(20,	2, 1),
(21,	2, 0.26),
(1,	3, 0.02),
(2,	3, 0.94),
(3,	3, 0.03),
(4,	3, 0.15),
(5,	3, 0.02),
(6,	3, 0.90),
(7,	3, 0.47),
(8,	3, 0.65),
(9,	3, 0.19),
(10,	3, 0.60),
(11,	3, 0.00),
(12,	3, 0.34),
(13,	3, 0.03),
(14,	3, 7.50),
(15,	3, 0.10),
(16,	3, 0.15),
(17,	3, 1.30),
(18,	3, 0.30),
(19,	3, 0.07),
(20,	3, 0.75),
(21,	3, 0.26)
;
TRUNCATE TABLE Supermarket_Ingridients;

SELECT*FROM Supermarket_Ingridients;


SELECT 
S.name as Supermarket,
I.name as Ingridient,
SM_Price as Price
FROM Supermarket_Ingridients as SI
LEFT JOIN Supermarkets as S ON SI.Supermarket_ID = S.ID
LEFT JOIN Ingridients as I ON SI.Ingridient_ID = I.ID
;

USE Brunch;
CREATE TABLE Dish_Supermarket_Price 
(ID INT AUTO_INCREMENT 
primary key NOT NULL,
Supermarket_ID INT, FOREIGN KEY (Supermarket_ID) REFERENCES Supermarkets(ID),
Dish_ID INT, FOREIGN KEY (Dish_ID) REFERENCES Dishes(ID),
SM_Dish_Price Float)
;

SELECT*FROM Dish_Supermarket_Price;

INSERT INTO Dish_Supermarket_Price
(Supermarket_ID, Dish_ID, SM_Dish_Price)
VALUES
(1,	1	,0.96),
(1,	2	,4.03),
(1,	3	,12.50),
(1,	4	,2.37),
(2,	1	,1.39),
(2,	2	,3.65),
(2,	3	,10.41),
(2,	4	,2.64),
(3,	1	,1.16),
(3,	2	,3.90),
(3,	3	,13.20),
(3,	4	,2.38)
;


SELECT 
S.name as NameOfSupermarket,
D.name as NameOfDish,
SM_Dish_Price as Price
FROM Dish_Supermarket_Price AS DSP
LEFT JOIN  Supermarkets as S ON DSP.Supermarket_ID = S.ID
LEFT JOIN Dishes as D ON DSP.Dish_ID = D.ID
;


SELECT 
D.name as NameOfDish,
S.name as NameOfSupermarket,
SM_Price as SupermarketPrice,
BP.name as NameOfRestaurant,
BP_Price as BrunchPlacePrice
FROM Dish_BrunchPlace_Supermarket_Prices AS PriceComparison
LEFT JOIN Dishes as D ON PriceComparison.Dish_ID = D.ID
LEFT JOIN  Supermarkets as S ON PriceComparison.Supermarket_ID = S.ID
LEFT JOIN BrunchPlaces as BP ON PriceComparison.BrunchPlace_ID = BP.ID; 
;

ALTER TABLE Ingridients
RENAME Ingredients; 

ALTER TABLE Supermarket_Ingridients
RENAME Supermarket_Ingredients; 

ALTER TABLE Dish_Ingridients
RENAME Dish_Ingredients; 

ALTER TABLE Dish_Ingredients
RENAME COLUMN Ingridient_ID to Ingredient_ID;

ALTER TABLE Supermarket_Ingredients
RENAME COLUMN Ingridient_ID to Ingredient_ID;


use brunch;

SELECT
	(	
		SELECT d.name
		FROM dishes d
		WHERE dsp.dish_id = d.id
	),
    (	
		SELECT s.name
		FROM Supermarkets s
		WHERE dsp.supermarket_id = s.id
	),
	dsp.SM_Dish_Price as SupermarketPrice,
	(	
		SELECT BP.name
		FROM Dish_BrunchPlaces dbp
		LEFT JOIN BrunchPlaces as BP ON dbp.BrunchPlace_ID = BP.ID
		WHERE dsp.Dish_ID = dbp.Dish_ID
        GROUP BY BP.name
	)
FROM Dish_Supermarket_Price as dsp;


---Supermarket price comparison ----

SELECT
	(	
		SELECT d.name
		FROM Dishes d
		WHERE dsp.Dish_ID = d.ID
	) AS DishName,
    (	
		SELECT s.name
		FROM Supermarkets s
		WHERE dsp.Supermarket_ID = s.ID
	) AS SupermarketName,
	dsp.SM_Dish_Price as SupermarketPrice
FROM Dish_Supermarket_Price as dsp;

---According to dish brunch place price catagorization.---

SELECT
	(	
		SELECT d.name
		FROM Dishes d
		WHERE dbp.Dish_ID = d.ID
	) AS DishName,
    (	
		SELECT bp.name
		FROM BrunchPlaces bp
		WHERE dbp.BrunchPlace_ID = bp.ID
	) AS BrunchLocation,
	dbp.price as RestaurantPrice
FROM Dish_BrunchPlaces as dbp;

--Price comparison between to dishes supermarkets and places. Merged  table do do the comparison. Dish_Supermarket_Price 
and Dish_BrunchPlace tables and created a grand table to see the price comparison.-

SELECT
    d.name AS DishName,
    s.name AS SupermarketName,
    dsp.SM_Dish_Price AS SupermarketPrice,
    bp.name AS BrunchLocation,
    dbp.price AS RestaurantPrice
FROM Dish_Supermarket_Price dsp
LEFT JOIN Dishes d ON dsp.dish_id = d.id
LEFT JOIN Supermarkets s ON dsp.supermarket_id = s.id
LEFT JOIN Dish_BrunchPlaces dbp ON dsp.dish_id = dbp.Dish_ID
LEFT JOIN BrunchPlaces bp ON dbp.BrunchPlace_ID = bp.ID
;


-What is the average price of the dishes according to supermarket and brunch Places--
--Average price ofthe supermarket dishes--
    
    SELECT
    d.name AS DishName,
    ROUND(AVG(dsp.SM_Dish_Price), 2) AS AveragePricePerSupermarket,
    ROUND(MAX(CASE WHEN s.name = 'Tesco' THEN dsp.SM_Dish_Price END), 2) AS TescoPrice,
    ROUND(MAX(CASE WHEN s.name = 'Morrison' THEN dsp.SM_Dish_Price END), 2) AS MorrisonPrice,
    ROUND(MAX(CASE WHEN s.name = 'Sainsbury' THEN dsp.SM_Dish_Price END), 2) AS SainsburyPrice
FROM
    Dish_Supermarket_Price dsp
JOIN
    Dishes d ON dsp.Dish_ID = d.ID
JOIN
    Supermarkets s ON dsp.Supermarket_ID = s.ID
GROUP BY
    d.name;
   
   
 -------Average price of dishes per brunch place---
   
SELECT
    d.name AS DishName,
    ROUND(AVG(dbp.Price), 2) AS AverageDishPrice,
    ROUND(MAX(CASE WHEN bp.name = 'The Astro Cafe' THEN dbp.price END), 2) AS TheAstroCafe,
    ROUND(MAX(CASE WHEN bp.name = 'Cafe 338' THEN dbp.price END), 2) AS Cafe338,
    ROUND(MAX(CASE WHEN bp.name = 'The Moonlight Cafe' THEN dbp.price END), 2) AS TheMoonlightCafe
FROM
    Dish_BrunchPlaces dbp
JOIN
    Dishes d ON dbp.Dish_ID = d.ID
JOIN
    BrunchPlaces bp ON dbp.BrunchPlace_ID = bp.ID
GROUP BY
    d.name;
    
    -----create an event and update the prices in dish_supermarket (Increase prices by 5% as an example) table every min.
    --run it, and then drop the event to see the result.
    
    SET GLOBAL event_scheduler = ON;

DELIMITER //
CREATE EVENT update_supermarket_prices
  ON SCHEDULE EVERY 1 minute
  STARTS CURRENT_TIMESTAMP
  DO
  BEGIN
    UPDATE Dish_Supermarket_Price
    SET SM_Dish_Price = SM_Dish_Price * 1.05;
  END;
//
DELIMITER ;

-- Create an event to update prices (Decrease prices by 5% as an example) in Dish_BrunchPlaces
-one MIN for the brunch places aswell to see if it is work and then drop the event.--

DELIMITER //
CREATE EVENT update_brunch_place_prices
  ON SCHEDULE EVERY 1 minute
  STARTS CURRENT_TIMESTAMP
  DO
  BEGIN
    UPDATE Dish_BrunchPlaces
    SET Price = Price * 0.95; 
  END;
//
DELIMITER ;


--DROPPING THE EVENTS--
DROP EVENT IF EXISTS update_brunch_place_prices ;
DROP EVENT IF EXISTS update_supermarket_prices;
