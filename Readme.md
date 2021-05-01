<p align="center">
  <img width="350" height="197" src="images/MySQL.png">
</p>

# Mysql
____This repository contains notes and examples__ to get started MySQL. 
## Introduction
To start w need to :
* Open XAMPP
![xampp](images/xampp.PNG?raw=true "xampp")
* open phpMyAdmin
http://localhost:8090/phpmyadmin
![phpMyAdmin](images/phpMyAdmin.PNG?raw=true "phpMyAdmin")
* moteur de stokage 
  * InnoDB
  * MyISAM


## CREATE 
CREATE DATABASE mydatabase;
DEFAULT CHARACTER SET utf8;
DEFAULT COLLATE utf8_general_ci;

	1)----- creation la table mytable
	CREATE TABLE mytable (
    	id int(11),
    	field1 varchar(100),
    	field2 varchar(100)
    	);

	2)----- création la table utilisateur2
	USE mydatabase;
	CREATE TABLE utilisateurs2(
    	nom VARCHAR(255) NOT NULL,
    	prenom VARCHAR(255) NOT NULL,
    	sexe VARCHAR(1) NOT NULL,
   	date_naissance DATA NOT NULL,
   	 
	)
    	ENGINE=INNODB;

	3)-----voir le code sql pour création une table
	USE mydatabase;
	SHOW CREATE TABLE utilisateurs;




## DROP 
DROP DATABASE mydatabase;
DROP TABLE utilisateurs2;

## DELETE 
DELETE FROM utilisateurs;
DELETE FROM utilisateurs WHERE nom='bounanoira';
DELETE FROM utilisateurs WHERE nom='bounaoira' LIMIT 1;
DELETE FROM utilisateurs WHERE id=6 LIMIT 1;
TRUNCATE TABLE utilisateurs;                            //suppprimer la table avec reintialisation l'id



## ALTER TABLE 
ALTER TABLE utilisateurs ADD ville VARCHAR(20) NOT NULL;
ALTER TABLE utilisateurs ADD pays VARCHAR(2) NOT NULL; 
ALTER TABLE utilisateurs ADD INDEX(sexe);
ALTER TABLE utilisateurs CHANGE date_naissance birthday DATE NOT NULL;
ALTER TABLE utilisateurs MODIFY birthday DATETIME NOT NULL;



## SELECT 
SELECT * FROM customers;
SELECT id,first_name,last_name FROM customers;
SELECT password FROM customers LIMIT 0,2;          //choisir 2 password à partir de 0
SELECT DISTINCT password FROM customers;          //flitre la répitation
SELECT * FROM customers LIMIT 10;	          //Afficher les 10 premier
SELECT * FROM customers ORDER BY id ASC;		  //Croissant
SELECT * FROM customers ORDER BY id DESC;	  //Descroissant
SELECT * FROM customers ORDER BY first_name;      //Alphabitique
SELECT friste_name FROM customers ORDER BY first_name;

## Count
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


## INSERT 
INSERT INTO customers(first_name,last_name,email,password,avatar,join_date) VALUES('Qannaf','AL-SAHMI','qannafalsahmi@gmail.com','1234','image/qannaf.jpg',NOW());
INSERT INTO customers(first_name,last_name) VALUES('Qannaf','AL-SAHMI');
		
		* ------- INSERT ++++ --------
		INSERT INTO customers(first_name,last_name,email,password,avatar,join_date) 
		VALUES
		('Qannaf','AL-SAHMI','qannafalsahmi@gmail.com','1234','image/qannaf.jpg',NOW()),
		('Qannaf1','AL-SAHMI1','qannafalsahmi@gmail.com','1234','image/qannaf.jpg',NOW());
		
		* -------2éme Méthode -------------
		INSERT INTO utilisateurs SET
			nom='bounaoara', 
            		prenom='rina', 
            		sexe='F';
	

## UPDATE 
UPDATE customers SET password='azerty';
UPDATE customers SET password='1234' WHERE first_name='Qannaf';
UPDATE customers SET password='1234' WHERE first_name='Qannaf' LIMIT 1;

## DELETE 
DELETE FROM customers WHERE first_name='Qannaf';


## WHERE 
SELECT * FROM customers WHERE last_name='smith';
SELECT * FROM customers WHERE id=18;
SELECT * FROM customers WHERE id<5;
SELECT * FROM customers WHERE id<5 AND last_name='smith';
SELECT * FROM customers WHERE id<5 OR last_name='smith';
SELECT * FROM customers WHERE (id<5 AND last_name='smith') OR first_name='Donald';
SELECT * FROM customers WHERE last_name IN ('Smith','Thompson')

## ALIAS 
SELECT email, password AS motdepasse FROM customers;    //changer le nome d'affichage pour password --> motdepasse
SELECT customer, CONCAT(address,'-',address2,'-',city,'-',state,':',zipcode) FROM customer_addresses;       
SELECT customer, CONCAT(address,'-',address2,'-',city,'-',state,':',zipcode) AS adress_Complete FROM customer_addresses;

## JOIN 
SELECT product_categories.name, products.name FROM product_categories INNER JOIN products ON product_categories.id=products.category;	   //jointure seulement
SELECT product_categories.name, products.name FROM product_categories LEFT JOIN products ON product_categories.id=products.category;       //Toutes les catégorie
SELECT product_categories.name, products.name FROM product_categories RIGHT JOIN products ON product_categories.id=products.category;
SELECT pc.name, p.name FROM product_categories AS pc RIGHT JOIN products AS p ON pc.id=p.category;
SELECT pc.name AS categoryName, p.name AS productsName FROM product_categories AS pc RIGHT JOIN products AS p ON pc.id=p.category;


## FUNCTION 
		1) Fuction Numérique
			SELECT *,SQRT(prix) FROM tableau;

		2) Fuction Texte
		  CONCAT          SELECT *, CONCAT(prenom,'',nom) AS nomPrenom  FROM utilisateurs;
                  LENGTH          SELECT *, LENGTH(prenom) AS taille  FROM utilisateurs;
	          LIKE            SELECT *  FROM utilisateurs WHERE prenom LIKE 'q%';
		  LOWER           SELECT *,LOWER(prenom) AS prenomMini FROM utilisateurs ;
	          UPPER 	  SELECT *,UPPER(prenom) AS prenomMax FROM utilisateurs ;
		  SUBSTR          SELECT *,SUBSTR(prenom,3) AS troisChar FROM utilisateurs ;
				  SELECT *,SUBSTR(prenom,3,1) AS troisChar FROM utilisateurs ;
		  REPLACE         SELECT *,REPLACE(prenom,'qannaf','ahmed') AS remplacerNom FROM utilisateurs ;
	          SOUNDEX	  SELECT *,SOUNDEX(prenom) FROM utilisateurs;
	          REVERSE         SELECT *,REVERSE(prenom) FROM utilisateurs;
		  TRIM            SELECT *,TRIM('             bar      ') FROM utilisateurs;
			          SELECT *,TRIM(BOTH 'x' FROM 'xxxxxbarxxxxxxxxx') FROM utilisateurs;
				  SELECT *,TRIM(LEADING 'x' FROM 'xxxxxbarxxxxxxxxx') FROM utilisateurs;
                                  SELECT *,TRIM(TRAILING 'x' FROM 'xxxxxbarxxxxxxxxx') FROM utilisateurs;
		3) Fuction Date
		 ADDDATE          SELECT *,ADDDATE(birthday, 10) AS jouter10jours FROM utilisateurs;
		 SUBDATE          SELECT *,SUBDATE(birthday, 10) AS jouter10jours FROM utilisateurs;
		 ADDTIME          SELECT *,ADDTIME(birthday, "1 01:00:00") AS jouter10jours FROM utilisateurs;
		 SUBTIME          SELECT *,SUBTIME(birthday, "1 01:00:00") AS jouter10jours FROM utilisateurs;
		 NOW              SELECT *,NOW() AS tempsCeJours FROM utilisateurs;                            //year/mois/jour h:m:s
		 CURDATE          SELECT *,CURDATE() AS tempsCeJours FROM utilisateurs;   //yeae/mois/jours
		 CCURTIME         SELECT *,CURTIME() AS tempsCeJours FROM utilisateurs;   //h:m:s
		 DATEDIFF         SELECT *,DATEDIFF(CURDATE(),birthday) AS numJours FROM utilisateurs;
		 FROM_DAYS        SELECT *,FROM_DAYS(DATEDIFF(CURDATE(),birthday)) AS numYears FROM utilisateurs;
                                  SELECT *,TRIM(LEADING '0' FROM FROM_DAYS(DATEDIFF(CURDATE(),birthday)))  AS numYears FROM utilisateurs;
		 DATE             SELECT * ,DATE('2020-03-03 01:34:45') AS temps FROM utilisateurs;
		 DATE_FORMAT      SELECT * ,DATE_FORMAT(birthday,"%W %d %Y") AS temps FROM utilisateurs ;
                 YEAR             SELECT * ,YEAR(birthday) AS yearsB FROM utilisateurs;
				  SELECT COUNT(*) ,YEAR(birthday) AS pubilation FROM utilisateurs GROUP BY YEAR(birthday);
				  SELECT 
					COUNT(*) ,
        				YEAR(birthday) AS y,
        				MONTH(birthday) AS m
					DAY(birthday) AS j
				  FROM utilisateurs 
				  GROUP BY 
        				y,
        				m,
					j
 

## DUMPS 
importer et exporter 
        
        

## JOINTURES DETAILS 
		SELECT * FROM t1 RIGHT JOIN t2 ON t1.id=t2.id
                SELECT * FROM t1 LEFT JOIN t2 ON t1.id=t2.id 
                SELECT * FROM t1 INNER JOIN t2 ON t1.id=t2.id 
                SELECT * FROM products RIGHT JOIN product_categories ON products.category=product_categories.id
         

## UNION
		SELECT * FROM t1
			UNION              //concatener les 2 tableaux
		SELECT * FROM t2
		


## SQL AVANCE 
	1) Fonction Date et d'heures
	   EXTRACT(month FROM "2020/04/08")

