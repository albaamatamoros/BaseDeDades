# ACTIVITAT - EXERCICIS $GROUP

1. Mostra la quantitat d’empleats per cada departament. Mostra id de departament i la quantitat.

Stage 1:

```js
db.empleats.aggregate([
    {
        $group: {
            _id: '$departament.codi',
            numEmpleats: { $sum : 1 }
        }
    }
]);

```

$group Stage 1:

```js
{
  _id: "$departament.codi",
  numEmpleats: {
    $sum: 1
  }
}
```

2. Si no ho has tingut en compte en l’exercici anterior. Només tingues en compte aquells empleats que estiguin en un departament.

Stage1 + Stage 2:

```js
db.empleats.aggregate(
  [
    {
      $group: {
        _id: '$departament.codi',
        numEmpleats: { $sum: 1 }
      }
    },
    { $match: { _id: { $ne: null } } }
]
);
```
$match Stage 2

```js
{
  _id: {"$ne": null}
}
```

3. Ordena el resultat anterior per els departament de més a menys nombre d’empleats.

Stage1 + Stage 2 + Stage 3 (complet):

```js
db.empleats.aggregate(
  [
    {
      $group: {
        _id: '$departament.codi',
        numEmpleats: { $sum: 1 }
      }
    },
    { $match: { _id: { $ne: null } } },
    { $sort: { numEmpleats: -1 } }
  ]
);
```

$sort Stage 3:

```js
{
 	numEmpleats : -1
}
```

4. De cada departament mostra el salari més alt. Mostra id de departament i el salari més alt.

```js
db.empleats.aggregate([
    {
        $group: {
            _id: "$departament.codi",
            maxSalari : {$max : "$salari" }
        }
    }
]);

//Stage

{
  _id: "$departament.codi",
  maxSalari : {$max : "$salari" }
}
```

5. Quina és la massa salarial de cada departament? Mostra id de departament i la massa salarial.

```js

```

6. Només mostra aquells departaments que tinguin una massa salarial igual o superior a 19000

```js
```
