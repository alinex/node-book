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

__Command concatenation__

If this should be done, don´t define the return type as the current class. Better
use `this` as return type which will also work if a subclass calls methods from
it´s superclass:

```js
/* @flow */

class A {
  x(): this {
    return this;
  }
}

class B extends A {
  y(): this {
    return this;
  }
}

var w = new B();

w.x().y();
```
