# ACTIVITAT - EXERCICIS PROCEDIMENTS

Exercici 7 - Volem fer un registre dels usuaris que entren al nostre sistema. Per fer-ho
primer caldrà crear una taula amb dos camps, un per guardar l’usuari i l’altre per guardar
la data i hora de l’accés.

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