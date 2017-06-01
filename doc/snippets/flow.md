# Flow annotations

You have to start each file with `// @flow` as the first comment line.


## Classes

__Declare properties__

It is necessary to define each used property. This not only helps in type analyzation
but also to make it more readable:

```js
// @flow
class SchemaAny {

  data: any

  constructor(data: any) {
    this.data = data
  }
}
```
