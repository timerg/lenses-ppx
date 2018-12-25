

# Build
```
npm run build
```

# Watch

```
npm run watch
```

In
```reason
module FormConfig = {
  [%lenses]
  type state = {
    email: string,
    age: int,
  };
}
```

Out

```reason
module FormConfig = {
  module StateLenses = {
    type state = {
      email: string,
      age: int,
    };
    type field(_) =
      | Email: field(string)
      | Age: field(int);
    let get: type value. (state, field(value)) => value =
      (state, field) =>
        switch (field) {
        | Email => state.email
        | Age => state.age
        };
    let set: type value. (state, field(value), value) => state =
      (state, field, value) =>
        switch (field) {
        | Email => {...state, email: value}
        | Age => {...state, age: value}
        };
  };
};
```