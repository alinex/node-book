# TypeScript

## Test

In testing typescript private members and functions are not accessible. You will
get a compile error. Netherless it will be accessible in the generated JacaScript
at the moment.

But for testing it is often needed to access them. This should be done by changing
the source code without really making the generated code complexer. To do this
I implemented it in the following solution.

Use the access modifiers as follows:
- public - completely accessible
- protected - things which should be available in extended classes or test
- private - something you only need in the class

As you see I use the protected for something needed in test like:

```js
class Work {
  protected load: integer
  constructor() {
    this.load = 1
  }
}
exports default Work
```

Now to access the `load` property I use a wrapper class within the test folder
(so it will not go into the dist):

```js
import * as Work from "../../src/Work"
class TWork extends Work {
  public getLoad(): integer {
    return this.load
  }
}
exports default TWork
```

Now within the test I use the added `getLoad()` method:

```js
import * TWork from "../wrapper/TWork"
const work = new TWork()
expect(work.getLoad()).to.equal(1)
```

The directory structure used looks like:

    src/Work.ts
    test/
      mocha/test.ts
      wrapper/TWork.ts
    dist/Work.js
