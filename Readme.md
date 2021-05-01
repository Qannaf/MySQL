<p align="center">
  <img width="350" height="197" src="images/MySQL.png">
</p>

# Mysql
__This repository contains notes and examples__ to get started MySQL. 

## Table of Contents
1. [Introduction](#Introduction)  
	1. [XAMPP](#XAMPP)
	1. [phpMyAdmin](#phpMyAdmin)
1. [CREATE ](#CREATE) 
1. [DROP](#DROP)
1. [DELETE](#DELETE)
1. [ALTER TABLE](#ALTER_TABLE)
1. [SELECT](#SELECT)
1. [Count](#Count)
1. [INSERT](#INSERT)
1. [UPDATE](#UPDATE)
1. [DELETE](#DELETE)
1. [WHERE](#WHERE)
1. [ALIAS](#ALIAS)
1. [JOIN](#JOIN)
1. [FUNCTION](#FUNCTION)
	1. [Fuction Numérique](#Fuction_Numerique)
	1. [Fuction Texte](#Fuction_Texte)
	1. [Fuction Date](#Fuction_Date)	
1. [DUMPS](#DUMPS)
1. [JOINTURES DETAILS](#JOINTURES_DETAILS)
1. [UNION](#UNION)
1. [SQL AVANCE](#SQL_AVANCE)


 
<a name="Introduction"></a>
## Introduction
To start we need to 
<a name="XAMPP"></a>:
* Open XAMPP \n
![xampp](images/xampp.PNG?raw=true "xampp")

<a name="phpMyAdmin"></a>
* open phpMyAdmin
http://localhost:8090/phpmyadmin
![phpMyAdmin](images/phpMyAdmin.PNG?raw=true "phpMyAdmin")
* moteur de stokage 
  * InnoDB
  * MyISAM

<a name="CREATE"></a>
## CREATE 
* CREATE DATABASE
```
CREATE DATABASE mydatabase;
DEFAULT CHARACTER SET utf8;
DEFAULT COLLATE utf8_general_ci;
```

  * creation la table mytable
	CREATE TABLE mytable (
    	id int(11),
    	field1 varchar(100),
    	field2 varchar(100)
    	);

  * création la table utilisateur2
	USE mydatabase;
	CREATE TABLE utilisateurs2(
    	nom VARCHAR(255) NOT NULL,
    	prenom VARCHAR(255) NOT NULL,
    	sexe VARCHAR(1) NOT NULL,
   	date_naissance DATE NOT NULL,
   	 
	)
    	ENGINE=INNODB;

  * voir le code sql pour création une table
	USE mydatabase;
	SHOW CREATE TABLE utilisateurs;



<a name="DROP"></a>
## DROP
``` 
DROP DATABASE mydatabase;
DROP TABLE utilisateurs2;
```

<a name="DELETE"></a>
## DELETE 
	DELETE FROM utilisateurs;
	DELETE FROM utilisateurs WHERE nom='bounanoira';
	DELETE FROM utilisateurs WHERE nom='bounaoira' LIMIT 1;
	DELETE FROM utilisateurs WHERE id=6 LIMIT 1;
	TRUNCATE TABLE utilisateurs;                            //suppprimer la table avec reintialisation l'id


<a name="ALTER_TABLE"></a>
## ALTER TABLE 
```
ALTER TABLE utilisateurs ADD ville VARCHAR(20) NOT NULL;
ALTER TABLE utilisateurs ADD pays VARCHAR(2) NOT NULL; 
ALTER TABLE utilisateurs ADD INDEX(sexe);
ALTER TABLE utilisateurs CHANGE date_naissance birthday DATE NOT NULL;
ALTER TABLE utilisateurs MODIFY birthday DATETIME NOT NULL;
```

<a name="SELECT"></a>
## SELECT 
```
SELECT * FROM customers;
SELECT id,first_name,last_name FROM customers;
SELECT password FROM customers LIMIT 0,2;          //choisir 2 password à partir de 0
SELECT DISTINCT password FROM customers;          //flitre la répitation
SELECT * FROM customers LIMIT 10;	          //Afficher les 10 premier
SELECT * FROM customers ORDER BY id ASC;		  //Croissant
SELECT * FROM customers ORDER BY id DESC;	  //Descroissant
SELECT * FROM customers ORDER BY first_name;      //Alphabitique
SELECT friste_name FROM customers ORDER BY first_name;
```

<a name="Count"></a>
## Count
```
SELECT COUNT(*) FROM utilisateurs;
SELECT COUNT(*) AS poubilation FROM utilisateurs;
SELECT    COUNT(*) AS poubilation, 
	  sexe                       FROM utilisateurs GROUP BY sexe;
SELECT    COUNT(id) AS poubilation, 
	  sexe                       FROM utilisateurs GROUP BY sexe;
SELECT COUNT(*) AS poubilation, sexe FROM utilisateurs GROUP BY sexe HAVING sexe="h"
SELECT   MAX(birthday) AS poubilation  FROM utilisateurs;
SELECT * FROM utilisateurs WHERE ville='sanaa' AND nom='qannaf2';
SELECT * FROM `utilisateurs` WHERE nom LIKE'q%';    //commance
SELECT * FROM `utilisateurs` WHERE nom LIKE'%q%';   //contient
SELECT * FROM `utilisateurs` WHERE nom LIKE'%q';    //termine
SELECT * FROM utilisateurs WHERE id IN(1,4,5);
```
<a name="INSERT"></a>
## INSERT 
* Method 1
```
INSERT INTO customers(first_name,last_name,email,password,avatar,join_date) VALUES('Qannaf','AL-SAHMI','qannafalsahmi@gmail.com','1234','image/qannaf.jpg',NOW());
INSERT INTO customers(first_name,last_name) VALUES('Qannaf','AL-SAHMI');
```	
* INSERT ++++ 
```
INSERT INTO customers(first_name,last_name,email,password,avatar,join_date) 
VALUES
('Qannaf','AL-SAHMI','qannafalsahmi@gmail.com','1234','image/qannaf.jpg',NOW()),
('Qannaf1','AL-SAHMI1','qannafalsahmi@gmail.com','1234','image/qannaf.jpg',NOW());
```

* Method 3 
```
INSERT INTO utilisateurs SET
			nom='bounaoara', 
			prenom='rina', 
			sexe='F';
```
<a name="UPDATE"></a>
## UPDATE
``` 
UPDATE customers SET password='azerty';
UPDATE customers SET password='1234' WHERE first_name='Qannaf';
UPDATE customers SET password='1234' WHERE first_name='Qannaf' LIMIT 1;
```

<a name="DELETE"></a>
## DELETE 
```
DELETE FROM customers WHERE first_name='Qannaf';
```

<a name="WHERE"></a>
## WHERE 
```
SELECT * FROM customers WHERE last_name='smith';
SELECT * FROM customers WHERE id=18;
SELECT * FROM customers WHERE id<5;
SELECT * FROM customers WHERE id<5 AND last_name='smith';
SELECT * FROM customers WHERE id<5 OR last_name='smith';
SELECT * FROM customers WHERE (id<5 AND last_name='smith') OR first_name='Donald';
SELECT * FROM customers WHERE last_name IN ('Smith','Thompson')
```

<a name="ALIAS"></a>
## ALIAS 
```
SELECT email, password AS motdepasse FROM customers;    //changer le nome d'affichage pour password --> motdepasse
SELECT customer, CONCAT(address,'-',address2,'-',city,'-',state,':',zipcode) FROM customer_addresses;       
SELECT customer, CONCAT(address,'-',address2,'-',city,'-',state,':',zipcode) AS adress_Complete FROM customer_addresses;
```

<a name="JOIN"></a>
## JOIN 
```
SELECT product_categories.name, products.name FROM product_categories INNER JOIN products ON product_categories.id=products.category;	   //jointure seulement
SELECT product_categories.name, products.name FROM product_categories LEFT JOIN products ON product_categories.id=products.category;       //Toutes les catégorie
SELECT product_categories.name, products.name FROM product_categories RIGHT JOIN products ON product_categories.id=products.category;
SELECT pc.name, p.name FROM product_categories AS pc RIGHT JOIN products AS p ON pc.id=p.category;
SELECT pc.name AS categoryName, p.name AS productsName FROM product_categories AS pc RIGHT JOIN products AS p ON pc.id=p.category;
```

<a name="FUNCTION"></a>
## FUNCTION 
<a name="Fuction_Numerique"></a>
1. Fuction Numérique
	SELECT *,SQRT(prix) FROM tableau;

<a name="Fuction_Texte"></a>
1. Fuction Texte
	1. CONCAT
		```	
		SELECT *, CONCAT(prenom,'',nom) AS nomPrenom  FROM utilisateurs;
		```
    1. LENGTH          
		```
		SELECT *, LENGTH(prenom) AS taille  FROM utilisateurs;
		```
	1. LIKE            
		```
		SELECT *  FROM utilisateurs WHERE prenom LIKE 'q%';
		```
	1. LOWER           
		```
		SELECT *,LOWER(prenom) AS prenomMini FROM utilisateurs ;
		```
	1. UPPER 	  
		```
		SELECT *,UPPER(prenom) AS prenomMax FROM utilisateurs ;
		```
    1. SUBSTR          
		```
		SELECT *,SUBSTR(prenom,3) AS troisChar FROM utilisateurs ;
		SELECT *,SUBSTR(prenom,3,1) AS troisChar FROM utilisateurs ;
		```
	1. REPLACE         
		```
		SELECT *,REPLACE(prenom,'qannaf','ahmed') AS remplacerNom FROM utilisateurs ;
		```
	1. SOUNDEX	  
		```
		SELECT *,SOUNDEX(prenom) FROM utilisateurs;
		```
	1. REVERSE         
		```
		SELECT *,REVERSE(prenom) FROM utilisateurs;
		```
	1. TRIM            
		```
		SELECT *,TRIM('             bar      ') FROM utilisateurs;
		SELECT *,TRIM(BOTH 'x' FROM 'xxxxxbarxxxxxxxxx') FROM utilisateurs;
		SELECT *,TRIM(LEADING 'x' FROM 'xxxxxbarxxxxxxxxx') FROM utilisateurs;
        SELECT *,TRIM(TRAILING 'x' FROM 'xxxxxbarxxxxxxxxx') FROM utilisateurs;
		```

<a name="Fuction_Date"></a>
1. Fuction Date
	1. ADDDATE          
		```
		SELECT *,ADDDATE(birthday, 10) AS jouter10jours FROM utilisateurs;
		```
	1. SUBDATE          
		```
		SELECT *,SUBDATE(birthday, 10) AS jouter10jours FROM utilisateurs;
		```
	1. ADDTIME          
		```
		SELECT *,ADDTIME(birthday, "1 01:00:00") AS jouter10jours FROM utilisateurs;
		```
	1. SUBTIME          
		```
		SELECT *,SUBTIME(birthday, "1 01:00:00") AS jouter10jours FROM utilisateurs;
		```
	1. NOW              
		```
		SELECT *,NOW() AS tempsCeJours FROM utilisateurs;                            //year/mois/jour h:m:s
		```
	1. CURDATE          
		```
		SELECT *,CURDATE() AS tempsCeJours FROM utilisateurs;   //yeae/mois/jours
		```
	1. CURTIME         
		```
		SELECT *,CURTIME() AS tempsCeJours FROM utilisateurs;   //h:m:s
		```
	1. DATEDIFF         
		```
		SELECT *,DATEDIFF(CURDATE(),birthday) AS numJours FROM utilisateurs;
		```
	1. FROM_DAYS        
		```
		SELECT *,FROM_DAYS(DATEDIFF(CURDATE(),birthday)) AS numYears FROM utilisateurs;
		SELECT *,TRIM(LEADING '0' FROM FROM_DAYS(DATEDIFF(CURDATE(),birthday)))  AS numYears FROM utilisateurs;
		```
	1. DATE             
		```
		SELECT * ,DATE('2020-03-03 01:34:45') AS temps FROM utilisateurs;
		```
	1. DATE_FORMAT      
		```
		SELECT * ,DATE_FORMAT(birthday,"%W %d %Y") AS temps FROM utilisateurs ;
		```
	1. YEAR             
		```
		SELECT * ,YEAR(birthday) AS yearsB FROM utilisateurs;
		SELECT COUNT(*) ,YEAR(birthday) AS pubilation FROM utilisateurs GROUP BY YEAR(birthday);
		SELECT COUNT(*) ,YEAR(birthday) AS y,
						 MONTH(birthday) AS m, 
						DAY(birthday) AS j
		  FROM utilisateurs 
						GROUP BY y,m,j;
		```
 
 
<a name="DUMPS"></a>
## DUMPS
``` 
importer et exporter 
```
        
        
<a name="JOINTURES_DETAILS"></a>
## JOINTURES DETAILS
``` 
SELECT * FROM t1 RIGHT JOIN t2 ON t1.id=t2.id
SELECT * FROM t1 LEFT JOIN t2 ON t1.id=t2.id 
SELECT * FROM t1 INNER JOIN t2 ON t1.id=t2.id 
SELECT * FROM products RIGHT JOIN product_categories ON products.category=product_categories.id         
```
<a name="UNION"></a>
## UNION
```
SELECT * FROM t1
	UNION              //concatener les 2 tableaux
SELECT * FROM t2
```

<a name="SQL_AVANCE"></a>
## SQL AVANCE 

1. Fonction Date et d'heures
```
EXTRACT(month FROM "2020/04/08")
```

