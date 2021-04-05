## AlgoeDB
A light, Embeddable, NoSQL database written in Go. 

Inspired by (and wherever possible a port of) the Deno project [AloeDB](https://github.com/Kirlovon/AloeDB). Many thanks to [@Kirlovon](https://github.com/Kirlovon) for the inspiration!

## Features
* 🎉 Simple to use API, similar to [MongoDB](https://www.mongodb.com/)!
* 🚀 Optimized for a large number of operations.
* ⚖  No dependencies outside of the standard library.
* 📁 Stores data in readable JSON file.

## Examples Usage

```go
config := AlgoeDB.DatabaseConfig{Path: "/path/to/file.json"}
db, err := AlgoeDB.NewDatabase(&config)
if err != nil {
    log.Fatal(err)
}

people := []map[string]interface{}{}
people = append(people, map[string]interface{}{"name": "Billy", "age": 27})
people = append(people,  map[string]interface{}{"name": "Carisa", "age": 26})

err = db.InsertMany(people)
if err != nil {
    log.Fatal(err)
}

query := map[string]interface{}{"name": "Carisa"}
results := db.FindMany(query)

if results != nil {
    fmt.Println("results:", results) //results: [map[age:26 name:Carisa]]
} else {
    fmt.Println("no documents found")
}

query = map[string]interface{}{"age": AlgoeDB.MoreThan(26)}
results = db.FindMany(query)

if results != nil {
    fmt.Println("results:", results) //results: [map[age:27 name:Billy]]
} else {
    fmt.Println("no documents found")
}
```