# ACTIVITAT - EXERCICIS CONSULT

1. Obtenir de tots els empleats, el nom, cognoms i salari. Mostrar només 4 registres

```json
db.empleats.find({}, {nom: 1, cognoms: 1, salari: 1} ).limit(5)
```
2. Mostra la quantitat de departaments que hi ha

```json
db.departaments.find().count()
```

3. Recupera l’empleat “emplat_id=100”

```json
db.departaments.find({ empleat_id: "100"})
```

4. Recupera els empleats amb el càrrec de “President”

```json
db.departaments.find({ "feina.nom" : "100"})
```

5. Recupera els empleats que treballen al departament de “IT”

6. Recupera els empleats que van ser contractats a partir de l’1 de gener de 1985

7. Recupera els empleats amb un salari superior a 2000

8. Recupera els empleats amb un salari entre 2000 i 6000

9. Recupera els empleats que el seu número de telèfon comença per 515

10. Recupera els empleats que no treballin de Vice President. Utilitza el codi de la feina
"AD_VP"

11. Recupera els empleats que tenen pct_comissio.

12. Recupera els empleats que tenen pct_comissio i hagi treballat o treballin
actualment de "Cap de Vendes" . Utilitza el codi de feina "SA_MAN".

13. Recupera els empleats que han tingut 2 feines. No tinguis en compte la feina
actual.