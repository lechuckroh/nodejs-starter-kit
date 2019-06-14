# Express.js + GraphQL

## Run
```bash
# install dependencies
$ npm install

# start json-server
$ npm run json-server

# start server in watch mode
$ npm run dev
```

Open `http://localhost:4000/graphql`.

## Example
### Query company by id with related users
```javascript
{
  company(id: "2") {
    name
    description
    users {
      firstName
      age
    }
  }
}

// Result
{
  "data": {
    "company": {
      "name": "Google",
      "description": "search",
      "users": [
        {
          "firstName": "Bar",
          "age": 21
        },
        {
          "firstName": "FooBar",
          "age": 40
        }
      ]
    }
  }
}
```

### Fragments
Reuse fragment to reduce duplication.
```javascript
{
  apple: company(id: "1") {
    ...companyDetails
  }
  google: company(id: "2") {
    ...companyDetails
  }
}

fragment companyDetails on Company {
  name
  description
  users {
    firstName
    age
  }
}

// result
{
  "data": {
    "apple": {
      "name": "Apple",
      "description": "iphone",
      "users": [
        {
          "firstName": "Foo",
          "age": 20
        }
      ]
    },
    "google": {
      "name": "Google",
      "description": "search",
      "users": [
        {
          "firstName": "Bar",
          "age": 21
        },
        {
          "firstName": "FooBar",
          "age": 40
        }
      ]
    }
  }
}
```

### Mutations
```javascript
mutation {
  addUser(firstName: "Tom", age: 30) {
    id
    firstName
    age
  }
  
  updateUser(id: "23", firstName: "Jane") {
    id
    firstName
  }
  
  deleteUser(id: "23") {
    id
    firstName
  }
}

// result
{
  "data": {
    "addUser": {
      "id": "qvS63Bq",
      "firstName": "Tom",
      "age": 30
    },
    "updateUser": {
      "id": "23",
      "firstName": "Jane"
    },
    "deleteUser": {
      "id": null,
      "firstName": null
    }
  }
}
```

