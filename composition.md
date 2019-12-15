## Function Composition

```js
const str = "Innovation distinguishes between a leader and a follower.";

const trim = str => str.replace(/^\s*|\s*$/g, "");

const noPunct = str => str.replace(/[?.,!]/g, "");

const capitalize = str => str.toUpperCase();

const breakout = str => str.split(" ");

const noArticles = str => str !== "A" && str !== "AN" && str !== "THE";

const filterArticles = arr => arr.filter(noArticles);

console.log(filterArticles(breakout(capitalize(noPunct(trim(str))))));
```

**output:**
```
Info: Start process (7:41:37 PM)
[
  'INNOVATION',
  'DISTINGUISHES',
  'BETWEEN',
  'LEADER',
  'AND',
  'FOLLOWER'
]
Info: End process (7:41:37 PM)

```

---

## Function Composition (compose) R -> L

```js
const str = "Innovation distinguishes between a leader and a follower.";

const trim = str => str.replace(/^\s*|\s*$/g, "");

const noPunct = str => str.replace(/[?.,!]/g, "");

const capitalize = str => str.toUpperCase();

const breakout = str => str.split(" ");

const noArticles = str => str !== "A" && str !== "AN" && str !== "THE";

const filterArticles = arr => arr.filter(noArticles);

// Compose (R -> L)
const compose = function(...fns) {
  return function(x) {
    return fns.reduceRight((v, f) => {
      return f(v);
    }, x);
  };
};

const prepareString1 = compose(
  filterArticles,
  breakout,
  capitalize,
  noPunct,
  trim
);

console.log(prepareString1(str));

```

**output:**
```
Info: Start process (7:43:44 PM)
[
  'INNOVATION',
  'DISTINGUISHES',
  'BETWEEN',
  'LEADER',
  'AND',
  'FOLLOWER'
]
Info: End process (7:43:44 PM)

```

---

## Function Composition (compose) R -> L

```js
const str = "Innovation distinguishes between a leader and a follower.";

const trim = str => str.replace(/^\s*|\s*$/g, "");

const noPunct = str => str.replace(/[?.,!]/g, "");

const capitalize = str => str.toUpperCase();

const breakout = str => str.split(" ");

const noArticles = str => str !== "A" && str !== "AN" && str !== "THE";

const filterArticles = arr => arr.filter(noArticles);

// Pipe (L -> R)
const pipe = function(...fns) {
  return function(x) {
    return fns.reduce((v, f) => {
      return f(v);
    }, x);
  };
};

const prepareString2 = pipe(
  trim,
  noPunct,
  capitalize,
  breakout,
  filterArticles
);

console.log(prepareString2(str));

```

**output:**
```
Info: Start process (7:44:25 PM)
[
  'INNOVATION',
  'DISTINGUISHES',
  'BETWEEN',
  'LEADER',
  'AND',
  'FOLLOWER'
]
Info: End process (7:44:25 PM)

```
