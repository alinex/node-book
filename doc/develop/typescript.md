# TypeScript

TypeScript is a superset of JavaScript which primarily provides optional static typing, classes and interfaces. One of the big benefits is to enable IDEs to provide a richer environment for spotting common errors as you type the code.

Instead of only adding types to standard JavaScript like flow does TypeScript is a
language of its own. It is aimed for large projects to get more robust software,
while still being deployable as regular JavaScript.

I for myself find TypeScript better supported, better community and faster developing
so after my first steps with flow+babel I switched to TypeScript.

### Installation

First you need to install TypeScript:

```bash
$ npm install typescript ts-node @types/node --save-dev
```

To make it usable you also have to add a configuration file `tsconfig.json` in your
project root:

```json
{
  "compilerOptions": {
    "target": "es6",
    "module": "commonjs",
    "outDir": "dist",
    "declaration": true,
    "sourceMap": true,
    "removeComments": true,
    "strict": true,
    "noImplicitAny": true,
    "strictNullChecks": true,
    "noImplicitThis": true,
    "alwaysStrict": true,
    "noUnusedLocals": true,
    "noUnusedParameters": true,
    "noImplicitReturns": true,
    "noFallthroughCasesInSwitch": true
  },
  "files": [
    "./node_modules/@types/mocha/index.d.ts",
    "./node_modules/@types/node/index.d.ts"
  ],
  "include": [
    "src/**/*.ts"
  ],
  "exclude": [
    "node_modules"
  ]
}
```

### Usage

Now you can integrate it in your `package.json`:

```json
{
  "scripts": {
    "lint": "tslint -c tslint.json 'src/**/*.ts'",
    "test": "mocha -r ts-node/register test/mocha/**.ts",
    "coverage": "nyc mocha",
    "dev": "NODE_ENV=development nodemon --exec ./node_modules/.bin/ts-node -- ./src/index.ts",
    "build": "tsc",
    "start": "node dist/index",
    "prepublish": "npm run build"
  },
  "engines": {
    "node": ">=6"
  }  
}
```

Also specify the engines information to help people use your module in the right version.

This defines the transformation to:
1. Be used as JIT compiler in dev mode (run using `npm run dev`)
2. Be converted into ES6 code by running `npm run build` (into `dist` folder)
3. Everything in dist folder can be used without TypeScript
4. Before publishing to npm the `build` command is called automatically
