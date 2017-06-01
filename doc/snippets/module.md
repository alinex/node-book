# Module handling


## How to import

It depends on what the module is exporting. If the module exports a collection
of named exports you should use the collection import:

```js
import fs from 'fs' // works but not preferred
import * as fs from 'fs' // recommended
```

But the best way is to only import the methods you really need:

```js
import { readdirSync } from 'fs' // recommended
```
