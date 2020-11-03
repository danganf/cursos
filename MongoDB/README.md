# [MongoDB: Uma alternativa aos bancos relacionais tradicionais](https://cursos.alura.com.br/course/mongodb)

## Aula 1

* Acessando o cliente MongoDB:
> mongo

* Criando a base de dados use alunos

* Criando a coleção alunos:
> db.createCollection("alunos")

* Para inserir o aluno descrito utilizamos o comando insert():

```javascript
db.alunos.insert({
     "nome": "Felipe",
     "data_nascimento": new Date(1994, 02, 26),
     "notas": [10, 9, 4.5],
     "curso": {
         "nome": "Sistemas de informação"
     },
     "habilidades": [
         {
             "nome": "Inglês",
             "nível": "Avançado"
         }
     ] 
 })
```

***

* Uma situação onde o MongoDB é bastante usado é quando precisamos realizar buscas por proximidade, como, por exemplo, localizar a pizzaria mais próxima de você.

* Situações onde o uso do MongoDB não é indicado são cenários onde precisamos fazer muitas operações de agregação em uma única query, isso tem muito custo para o MongoDB.

***

* para listá-los, basta utilizar o comando find(), sem nenhum argumento:

> db.alunos.find()

* Para remover um aluno usamos o seguinte comando:

> db.alunos.remove({"_id": ObjectId("578b87a7239a421f908ed46b")})
* Perceba que o id pode variar. Este é apenas um exemplo com um id qualquer. Os que aparecem para você serão diferentes.

## Aula 2

* Para restringir as buscas no Mongo precisamos passar um exemplo, no caso {"nome": "Felipe"}, assim o Mongo busca todos que seguem o exemplo

```javascript
db.alunos.find({"nome":"Felipe"})
```

* Para buscar usando a clausula and, basta adicionar outro campo no json passado como exemplo

```javascript
db.alunos.find({"nome": "Felipe", "data_nascimento": new Date(1994, 02, 26)})
```

* No MongoDB conseguimos navegar em um documento através do .

```javascript
db.alunos.find({"habilidades.nome": "inglês"})
```

* Busque todos os alunos dos cursos de Sistemas de informação ou de Ciências da computação
    * Esse exercício pode ser resolvido através do uso dos operadores $or ou $in

```javascript
db.alunos.find({$or:
    [
        {"curso.nome": "Sistemas de informação"},
        {"curso.nome": "Ciências da computação"}

    ]
 }).pretty()
```
ou
```javascript
db.alunos.find({"curso.nome": {$in:
    [
        "Sistemas de informação",
        "Ciências da computação"
    ]
 }}).pretty()
```

## Aula 3

* Fazer uma substituição nada mais é do que fazer uma atualização no documento, então usamos update({"_id": "[id do documento]".... Aqui substituiremos o usuário do id abaixo pela Daniela:

```javascript
db.alunos.update({"_id": ObjectId("1234565435")}, 
{
    "nome": "Daniela",
    "data_nascimento": new Date(1997, 07, 17),
    "notas": [10, 9, 4],
    "curso": {
        "nome": "Moda"
    },
    "habilidades": [
        {
            "nome": "Alemão",
            "nível": "Básico"
        }
    ] 
}
)
```

* Para substituir somente um campo do documento basta usar o operador $set passando um json com o campo e o novo valor

```javascript
db.alunos.update({"curso.nome": "Moda"}, {$set:
{"curso.nome": "Administração"}
})
```

* Por padrão o método update só atualiza um documento, para que ele atualize mais de um precisamos passar também o parâmetro multi:true

```javascript
db.alunos.update({"curso.nome": "Moda"}, {$set:
{"curso.nome": "Administração"}}, {multi:true}
)
```

* Para adicionar um valor a um array já existente usamos o operador `$push`

```javascript
db.alunos.update({"nome":"Felipe"}, {$push:{notas: 8.5}})
```
* Para adicionar mais de um valor a um array já existente usamos o modificador $each em conjunto com o operador $push

```javascript
db.alunos.update({"nome":"Guilherme"}, {$push:{"notas":{$each:[8.5, 10]}}})
```

## Aula 4
* O Mongo DB nos oferece vários operadores que podem ser encontrados aqui https://docs.mongodb.org/manual/reference/operator/query/

* O operador que equivale ao "menor que" é o `$lt`

```javascript
db.alunos.find({"notas":{$lt:5}})
```

* Para limitar a quantidade de resultados podemos usar o método limit() passando a quantidade ou usar o método findOne() se a quantidade for 1
```javascript
db.alunos.findOne({"curso.nome":"Sistemas de informação"})
```
ou
```javascript
db.alunos.find({"curso.nome":"Sistemas de informação"}).limit(1)
```

* Para ordenar usamos o método sort() e passamos com parâmeto um JSON {nome do campo: ordem(1 para crescente e -1 para decrescente)}
```javascript
db.alunos.find().sort({"nome": 1})
```

## Aula 5

* alunos.json
```javascript
[
{
	"nome" : "Guilherme",
	"localizacao" : { "type" : "Point", "coordinates" : [-23.5882133, -46.63235580000003]}
},{
	"nome" : "Paulo",
	"localizacao" : { "type" : "Point", "coordinates" : [-23.5707855, -46.643499399999996]}
},
{
	"nome" : "Ana",
	"localizacao" : { "type" : "Point", "coordinates" : [-23.5829461, -46.6315126]}
},
{
	"nome" : "Carlos",
	"localizacao" : { "type" : "Point", "coordinates" : [-23.5834181, -46.6418552]}
},
{
	"nome" : "Lúcia",
	"localizacao" : { "type" : "Point", "coordinates" : [-23.5702415, -46.635375]}
},
{
	"nome" : "Stella",
	"localizacao" : { "type" : "Point", "coordinates" : [-23.5623743, -46.6478634]}
},
{
	"nome" : "Daniela",
	"localizacao" : { "type" : "Point", "coordinates" : [-23.5690615, -46.6592789]}
},
{
	"nome" : "Eduardo",
	"localizacao" : { "type" : "Point", "coordinates" : [-23.5552147, -46.6574764]}
},
{
	"nome" : "Felipe",
	"localizacao" : { "type" : "Point", "coordinates" : [-23.5606041, -46.6663599]}
},
{
	"nome" : "Marco",
	"localizacao" : { "type" : "Point", "coordinates" : [-23.5625317, -46.6686773]}
},
{
	"nome" : "Mariana",
	"localizacao" : { "type" : "Point", "coordinates" : [-23.5617056, -46.662454600000004]}
},
{
	"nome" : "Juliana",
	"localizacao" : { "type" : "Point", "coordinates" : [-23.5578111, -46.6656303]}
},
{
	"nome" : "Adriana",
	"localizacao" : { "type" : "Point", "coordinates" : [-23.5653639, -46.661725]}
},
{
	"nome" : "Roberto",
	"localizacao" : { "type" : "Point", "coordinates" : [-23.5549787, -46.6588497]}
},
{
	"nome" : "Marcelo",
	"localizacao" : { "type" : "Point", "coordinates" : [-23.5640265, -46.6527128]}
},
{
	"nome" : "Sofia",
	"localizacao" : { "type" : "Point", "coordinates" : [-23.5673307, -46.6529703]}
},
{
	"nome" : "Sheila",
	"localizacao" : { "type" : "Point", "coordinates" : [-23.5672914, -46.6462326]}
},
{
	"nome" : "William",
	"localizacao" : { "type" : "Point", "coordinates" : [-23.5803502, -46.6352892]}
},
{
	"nome" : "Manoela",
	"localizacao" : { "type" : "Point", "coordinates" : [-23.5831428, -46.6334867]}
}
]
```
* Para importar arquivos para o MongoDB usamos o comando mongoimportcom os parâmetros -c nome da coleção e --jsonArray < nome do arquivo .json

```sh
mongoimport -c alunos --jsonArray < alunos.json
```

* Para criar um índice usamos o método createIndex()

```javascript
db.alunos.createIndex({"localizacao": "2dsphere"})
```

* Para realizar busca por proximidade precisamos passar a coordenada, o tipo da coordenada (um ponto), o tipo do local onde a busca será realizada (esfera) e o nome do campo onde o mongo colocará a distância calculada
```javascript
db.alunos.aggregate([{
    $geoNear:{
        "near": {
            "coordinates":[-23.588055, -46.632403],
            "type":"Point"
},
"distanceField": "distancia.calculada",
"spherical": true
}
}])
```

* Para limitar a quantidade precisamos passar o campo `num: quantidade`
```javascript
db.alunos.aggregate([{
    "$geoNear":{
        "near": {
            "coordinates":[-23.588055, -46.632403],
            "type":"Point"
},
"distanceField": "distancia.calculada",
"spherical": true,
"num":4
}
}])
```

* Ignore o documento que tem o campo distancia.calculada com o valor 0
```javascript
db.alunos.aggregate([{
    "$geoNear": {
      "near": {
        "coordinates":[-23.588055, -46.632403],
        "type":"Point"
      },
    "distanceField": "distancia.calculada",
    "spherical": true
    }
  },
  { $skip: 1 }
]);
```