Testy
---
Fake objects <br>
Mock objects <br>
Stub objects <br>

Vavr
---
Biblioteka [vavr](http://www.vavr.io/) dodająca funkcyjne narzędzia do javy. 

```xml
<dependency>
    <groupId>io.vavr</groupId>
    <artifactId>vavr</artifactId>
    <version>0.9.1</version>
</dependency>
```

Immutowalne kolekcje. <br>
```java
List<String> names = List();
List<String> moreNames = names.add("Marcin");
// names różni się od moreNames, names nie zostało zmodyfikowane
```

Łatwiejsze przetwarzanie kolekcji. <br>
```java
List<String> oldPersons = persons
  .filter(p -> p.age > 12);

// w czystej javie trzeba napisać
List<String> oldPersons = persons
  .stream()
  .filter(p -> p.age > 12)
  .collect(toList());
```

Lombok
---
Biblioteka pozwalająca pozbyć się nadmiarowego kodu.

```xml
<dependency>
    <groupId>org.projectlombok</groupId>
    <artifactId>lombok</artifactId>
    <version>1.16.18</version>
    <scope>provided</scope>
</dependency>
```

Generacja immutowalnych klas.
```java
@Value
class Foo {
  private final String bar;
}

// w czystej javie
class Foo {
  private final String bar;
  
  Foo(String bar) {
    this.bar = bar;
  }
  
  String getBar() {...}
 
  boolean equals(Object object) {...}
  
  int hashCode() {...}
  
  String toString() {...}
}
```

Dedukcja typu
```java
val products = new HashMap<String, Product>();
val houses = new HashMap<String, House>();

// w czystej javie
Map<String, Product> products = new HashMap<>();
Map<String, House> houses = new HashMap<>();
```

Mongo instalacja
---
Obraz: https://hub.docker.com/_/mongo <br>

Klient mongo: https://docs.mongodb.com/getting-started/shell/installation <br>

**Postawienie mongo** <br>
`docker run -d -p 27017:27017 --name mongo mongo` <br>

**Podpięcie do mongo** <br>
`mongo` <br>
`docker exec -it mongo /usr/bin/mongo` <br>

Mongo komendy
---

**Wybranie bazy** <br>
`use test-db` <br>

**Utworzenie kolekcji** <br>
`db.createCollection('test')` <br>

**Wyświetl kolekcje** <br>
`db.getCollectionNames()` <br>
`show collections` <br>

**Wyświetl bazy** <br>
`show databases` <br>

**Umieść dokument** <br>
`db.test.insert({"test-key": 3})` <br>

**Wyświetl wszystkie dokumenty** <br>
`db.test.find({})` <br>

**Wyświetl wybrane dokumenty** <br>
`db.test.find({"test-key": {$gt: 2}})` <br>

**Modyfikuj dokument** <br>
`db.test.update({"_id": ObjectId("59ea60f491cc82d8272001bc")},{"test-key": 4})` <br>

Mongo klient java
---

```xml
<dependency>
  <groupId>org.mongodb</groupId>
  <artifactId>mongo-java-driver</artifactId>
  <version>3.5.0</version>
</dependency>
<dependency>
  <groupId>com.fasterxml.jackson.core</groupId>
  <artifactId>jackson-databind</artifactId>
  <version>2.9.1</version>
</dependency>
<dependency>
  <groupId>io.vavr</groupId>
  <artifactId>vavr-jackson</artifactId>
  <version>0.9.1</version>
</dependency>
```

```java
MongoClient client = new MongoClient(mongoAddress, mongoPort);
MongoDatabase mongoDatabase = mongoClient.getDatabase(dbName);
MongoCollection mongoCollection = mongoDatabase.getCollection(collectionName);
```


Zadanie 1
------

1. Utwórz bazę shops i kolekcję shops. <br>

```json
{
  "name": "sklep",
  "products": ["a", "b"]
}
```


Umieść sklepy z produktami.

Wyjmij sklepy w których jest dany produkt.

Zadanie 2
------

1. Stwórz aplikację pozwalającą na umieszczanie w mongo sklepów i ją zdokeryzuj. <br>

```json
{
  "id": "some-shop",
  "products": [
    {
      "id": "some-product",
      "price": 10
    }
  ]
}
```
