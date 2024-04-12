#ACTIVITAT - EXERCICIS PROCEDIMENTS
-- EX7
```mysql
DROP PROCEDURE IF EXISTS spRegistrarUsuari;
DELIMITER //
CREATE PROCEDURE spRegistrarUsuari()
BEGIN
    INSERT INTO registre_usuaris(usuari,access)
    VALUES(CURRENT_USER(), NOW());
END
//
CALL spRegistrarUsuari()//
```