# ACTIVITAT - EXERCICIS SUBPROGRAMES

Exercici 1 - Fes una funció anomenada spData, tal que donada una data en format MySQL ( AAAA-MM-DD ) ens retorni una cadena de caràcters en format DD-MM-AAAA

Exemple : SELECT spData('1988-12-01') => 01-12-1988

```mysql
DELIMITER //
DROP FUNCTION IF EXISTS spData //
CREATE FUNCTION spData(pData DATE) RETURNS CHAR(10)
DETERMINISTIC
BEGIN
	DECLARE vRetorn CHAR(10);
    
    SET vRetorn = date_format(pData, "%d-%m-%Y");
    
    RETURN vRetorn;
END
//
DELIMITER;
```

Exercici 2 - Fes una funció anomenada spPotencia, tal que donada una base i un exponent, ens calculi la seva potència. Intenta no utilitzar la funció POW.

Exemple : SELECT spPotencia(2,3) => 8

```mysql
DELIMITER //
DROP FUNCTION IF EXISTS spPotencia //
CREATE FUNCTION spPotencia(pBase INT, pExp INT) RETURNS BIGINT
DETERMINISTIC
BEGIN
	DECLARE vRetorn BIGINT;
    
    IF pBase IS NOT NULL AND pExp IS NOT NULL THEN
		SET vRetorn = 1;
        WHILE pExp > 0 DO
			SET vRetorn = vRetorn * pBase;
            SET pExp = pExp -1;
		END WHILE;
        END IF;
    
    RETURN vRetorn;
END
//
DELIMITER;
```

Exercici 3 - Fes una funció anomenada spIncrement que donat un codi d’empleat i un % de increment, ens calculi el salari sumant aquest percentatge.

Per exemple, suposem que l’ empleat amb id_empleat = 124 té un salari de 1000

Exemple: SELECT spIncrement(124,10) obtindriem -> 1100

```mysql
DELIMITER //
DROP FUNCTION IF EXISTS spIncrement //
CREATE FUNCTION spIncrement(pEmpleatId INT, pIncrement FLOAT) RETURNS FLOAT
NOT DETERMINISTIC READS SQL DATA
BEGIN
	DECLARE vRetorn FLOAT;
    
    SELECT salari*(pIncrement + 100) /100 INTO vRetorn
		FROM empleats
	WHERE empleat_id = pEmpleatId;
    
    RETURN vRetorn;
END
//
DELIMITER;
```

Exercici 4 - Fes una funció anomenada spPringat, tal que li passem un codi de departament, i ens torni el codi d’empleat que guanya menys d’aquell departament. 

```mysql
DELIMITER //
DROP FUNCTION IF EXISTS spPringat //
CREATE FUNCTION spPringat(pDepartamentId INT) RETURNS INT
NOT DETERMINISTIC READS SQL DATA
BEGIN
	DECLARE vRetorn  INT;
    
    SELECT empleat_id INTO vRetorn
		FROM empleats
	WHERE departament_id = pDepartamentId
    ORDER BY pDepartamentId
    LIMIT 1;
    
    RETURN vRetorn;
END
//
DELIMITER;
```

Exercici 5 - Utilitzant la funció spPringat fes una consulta per obtenir de cada departament, l’empleat pringat. 

Mostra el codi i nom del departament, i el codi d’empleat.

```mysql
SELECT rrhh.spPringat();
```

EXERCICI 6 Exercici 6 - Fes una funció anomenada spCategoria, tal que donat un codi d’empleat, ens digui en quina categoria professional està. 

El criteri que volem seguir per determinar la categoria professional és en funció dels anys que porta treballant a l’empresa:

Entre 0 i 1 anys -> Auxiliar

Entre 2 i 10 anys -> Oficial de Segona

Entre 11 i 20 Anys -> Oficial de Primera

Més de 20 anys -> Que es jubili!

```mysql
DELIMITER //
DROP FUNCTION IF EXISTS spCategoria //
CREATE FUNCTION spCategoria(pCodiEmpleat INT) RETURNS VARCHAR(20)
NOT DETERMINISTIC READS SQL DATA
BEGIN
	DECLARE vRetorn VARCHAR(20);
    DECLARE anys INT;
    
    SELECT YEAR(CURDATE()) - YEAR(data_contractacio) INTO anys
    FROM empleats
    WHERE empleat_id = pCodiEmpleat;
    
    SET vRetorn = CASE
	WHEN anys BETWEEN 0 AND 1 THEN "Auxiliar"
    WHEN anys BETWEEN 2 AND 10 THEN "Oficial de Segona"
    WHEN anys BETWEEN 11 AND 20 THEN "Oficial de Primera"
    ELSE "Que es jubili"
    END;
    
    RETURN vRetorn;
END //
DELIMITER ;

SELECT spCategoria(207);
```

Exercici 7 - Fes una consulta utilitzant la funció anterior perquè mostri mostri de cada empleat, el codi d’empleat, el nom, els anys treballats i la categoria professional a la que
#pertany.

```mysql
SELECT empleat_id, nom, cognoms, spCategoria(empleat_id)
	FROM empleats;
```

Exercici 8 - Fes una funció anomenada spEdat, tal que donada una data per paràmetre ens retorni l'edat d'una persona. 

Les dates posteriors a la data d'avui han de retornar 0.

```mysql
DELIMITER //
DROP FUNCTION IF EXISTS spEdat //
CREATE FUNCTION spEdat(pDataIntroduida DATE) RETURNS INT UNSIGNED
NOT DETERMINISTIC READS SQL DATA
BEGIN
	DECLARE vRetorn INT UNSIGNED;
    
    SET vRetorn = CASE
		WHEN pDataIntroduida >= CURDATE() THEN 0
        ELSE YEAR(CURDATE()) - YEAR(pDataIntroduida) - (RIGHT(CURDATE(), 5) < RIGHT(pDataIntroduida, 5))
        END;
        RETURN vRetorn;
	END // 
DELIMITER ;

SELECT spEdat('2002-07-03');
```

Exercici 9 - Fes una funció que ens retorni el número de directors (caps) diferents tenim.

```mysql
DELIMITER // 
DROP FUNCTION IF EXISTS spNumDirectors //
CREATE FUNCTION spNumDirectors() RETURNS INT
NOT DETERMINISTIC READS SQL DATA
BEGIN
	DECLARE vRetorn INT;
    
    SELECT COUNT(DISTINCT empleat_id) INTO vRetorn
		FROM empleats
	WHERE feina_codi = 'AD_PRES';
    
	RETURN vRetorn;
END //
DELIMITER ;

SELECT spNumDirectors();
```

Exercici 10 - Quina instrucció utilitzarem si volem veure el contingut de la funció spPringat?

```mysql
SHOW CREATE FUNCTION spPringat;

SELECT * FROM information_schema.routines;
	

SHOW TABLES FROM information_schema;
```


