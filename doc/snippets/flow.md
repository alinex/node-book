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

__Uncheck by casting with any__

It's not a very nice solution, but you can cast an object to any. And no unsafe any will be leaked.

```js
/* @flow */

class A {
  get clone(): this {
//    return Object.assign(Object.create(this), this) // flow error
    return Object.assign((Object.create(this): any), this)
  }
}

class B extends A {}

var b = new B()
var c = b.clone
```

Here the `Object.create(this)` will normally give an error: Covariant property clone incompatible
with contravariant use in call of method assign.

The fix is it is casted by any.
