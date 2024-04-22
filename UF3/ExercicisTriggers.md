# ACTIVITAT - EXERCICIS TRIGGERS

Donada la base de dades de RRHH proporcionada pel professor realitza els
següents exercicis 

Exercici 1: Omplir la següent taula indicant en cada cas si es pot accedir als
registres NEW i OLD des del trigger corresponent i, en cas afirmatiu, quin tipus
d'operació és pot realitzar (L(llegir) o M(modificar)).


### INSERT:

|  | before | after |
| ----|---|---|
| NEW | M | X |
| OLD | X | X |

### DELETE:

|  | before | after |
| ----|---|---|
| NEW | X | X |
| OLD | L | X |

### UPDATE:

|  | before | after |
| ----|---|---|
| NEW | M | X |
| OLD | X | L |


Exercici 2: A quina taula o taules de la base de dades INFORMATION_SCHEMA de
MySQL es poden consultar els triggers que hi ha a la base dades?

```mysql
```
Exercici 3: Auditoria de la taula “empleats”
Crea el que creguis necessari per auditar la taula d’empleats. Aquesta auditoria
pretén dur un control automàtic dels canvis (INSERT, UPDATE, DELETE) que es
realitzen en aquesta taula.
Si no la tens crea una taula anomenada auditoria_taules amb els següents camps:

```mysql
```
Exercici 4: Validació de dades d’entrada
Mitjançant triggers volem dur el control de dades d’entrada d’una taula.
Concretament volem dur el control del camp salari de la taula empleats. Aquest
salari ha de ser un valor dins del rang marcat pels camps salari_min i
salari_max de la taula feines.
En definitiva, volem controlar que el salari dels empleats estigui dins dels rangs de
salaris marcats per el tipus de feina que fa l’empleat.

```mysql
DROP TRIGGER IF EXISTS trg_salari_empleats;
DELIMITER //
CREATE TRIGGER trg_salari_empleats BEFORE UPDATE ON empleats FOR EACH ROW
BEGIN
        IF((NEW.salari < (SELECT salari_min FROM feines WHERE feina_codi = NEW.feina_codi)) OR (NEW.salari > (SELECT salari_max FROM feines WHERE feina_codi = NEW.feina_codi))) THEN
                SET NEW.salari = OLD.salari;
    END IF;
END //

CREATE TRIGGER trg_salari_empleats_Insert BEFORE INSERT ON empleats FOR EACH ROW
BEGIN
        IF((NEW.salari < (SELECT salari_min FROM feines WHERE feina_codi = NEW.feina_codi)) OR (NEW.salari > (SELECT salari_max FROM feines WHERE feina_codi = NEW.feina_codi))) THEN
                SET NEW.salari = (SELECT salari_min FROM feines WHERE feina_codi = NEW.feina_codi);
    END IF;
END //
DELIMITER ;
```
Exercici 5: Manteniment del camp num_empleats
Afegeix un el camp num_empleats a la taula departaments. Aquest camp
simbolitza/modela el número d’empleats que té aquell departament.
Implementa mitjançant triggers el manteniment d’aquest camp de manera
automàtica.
Per exemple si s’afegeix un nou empleat del departament amb codi 10 cal
augmentar en 1 aquest camp del departament_id = 10

```mysql
```
Exercici 6: Manteniment de l’historial de feines
Implementa el que creguis necessari per mantenir la taula historial_feines de
forma automàtica. És dir, quan es s’afegeix o es modifica la feina d’un empleat, cal
registrar aquest canvi a la taula historial_feines.
Cal tenir en compte que si l’empleat canvia de departament no cal registrar-ho a la
taula historial_feines.
La data_inici i data_fi han d’anar en consonància a les dates del canvi de feina.

```mysql
```
# ACTIVITAT - EXERCICIS TRIGGERS (Part 2)

```mysql
```
