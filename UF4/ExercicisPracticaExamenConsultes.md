# ACTIVITAT - PARACTICA EXERCICIS

1. Volem comparar l'alçada dels dos germans Gasol. El noms curts són "Pau Gasol" i "Marc Gasol".

```js
db.jugadors.find({"nom_curt": {$in:["Pau Gasol","Marc Gasol"]}},{"nom_curt":1,"alcada":1,_id:0})
```

2. L’entrenador “Pedro Martínez” és un dels entrenadors més veterans. Quants partits ha participat com a entrenador. Independentment de si ho ha fet com a local o com a visitant. Restringeix la consulta als partits de lla Lliga Regular de la temporada 2023-2024.

```js
db.partits.countDocuments({
   $or: [
      { "equip_local.entrenadors.nom": "Pedro Martínez" },
      { "equip_visitant.entrenadors.nom": "Pedro Martínez" }
   ],
   "temporada": "2023-2024",
   "competicio": "Lliga Regular"
})
```

3. La llicència "JFL" indica que és un jugador de formació. Quants jugadors tenim amb aquesta llicència?.

## FIND

```js
db.jugadors.find({"llicencia": {$eq : "JFL"}}).count()

||

db.jugadors.find({"llicencia": "JFL"}).count()

```
## AGGREGATION F
```js

db.jugadors.aggregate([
  {
    $match: {
      llicencia: "JFL"
    }
  },
  {
    $count: "llicencia"
  }
]);

```

4. Passa a Decimal el camp alcada de la col·lecció jugadors. (https://www.mongodb.com/docs/manual/reference/operator/aggregation/convert/)

```js
db.jugadors.aggregate([
        {
            $convert: {
                alcada: {$toDecimal : "$alcada"}
            }
        }
    ]);
```

5. Quins jugadors tenim el compte d'Instagram? Mostra el nom_curt del jugador i l'usuari d'Instragram.

```js
```

6. Dona el número total de punts de l'equip local del partit amb codi_acb :"103778"

```js
```

7. Obtenir els punts de cada equip (local i visitant) del partit amb codi_acb: "103778"