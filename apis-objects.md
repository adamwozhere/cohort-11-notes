# JS API's and Objects / JSON

## API's

- Application Programming Interface; interface between the backend and frontend
  - in a restaurant the backend is the kitchen, waiter is the API, table / customer is the frontend
- REST API - most common, data is usually in JSON format
- API’s have several endpoints (URL’s) where the developer can access the data
- It is a 2-way process, you can POST and GET data (send and receive)
- Endpoint data usually comes back as JSON; you can parse the JSON into a JavaScript object using `JSON.parse()` and send a JavaScript object by turning it into JSON with `JSON.stringify()`

## Objects vs JSON

- Object literals look similar to JSON objects except they are not!
- JS objects follow `{ key: 'value' }` syntax
- JSON data follows `{ "key": "value" }` syntax - (keys are also in quotes)
- Values can contain other objects, or arrays of objects of values etc.

```
data.json

[
  {
    "key": "value"
  },
  {
    "key": "value
  },
  {
    "key": "value
  },
]
```

- As an Object Literal it would be very similar:

```
const myObj = [
  {
    key: 'value'
  },
  {
    key: 'value'
  },
  {
    key: 'value'
  },
];
```

- Appear to be able to convert between JSON and an Object / Array freely? it must know to convert to an array in the case of bringing in JSON?
- To view an Object or JSON easily in console etc. use `JSON.stringify(myObj, null, 2)`, where `myObj` is the object or JSON, `null` is the seprator, and `2` is the number of space indentation
