# ClassName

## Interview Question

Implémentez la fonction classnames.

## Description

Classnames est un utilitaire couramment utilisé dans les applications front-end modernes pour lier conditionnellement les noms de classes CSS. Si vous avez déjà développé des applications React, vous avez probablement utilisé une bibliothèque similaire.

### Exemple

```js
classNames("foo", "bar"); // 'foo bar'
classNames("foo", { bar: true }); // 'foo bar'
classNames({ "foo-bar": true }); // 'foo-bar'
classNames({ "foo-bar": false }); // ''
classNames({ foo: true }, { bar: true }); // 'foo bar'
classNames({ foo: true, bar: true }); // 'foo bar'
classNames({ foo: true, bar: false, qux: true }); // 'foo qux'
```

## Interview Solution

```js
/**
 * @param {...(any|Object|Array<any|Object|Array>)} args
 * @return {string}
 */
export default function classNames(...args) {
  const classes = [];
  function processArg(arg) {
    if (typeof arg === "string" && arg) {
      classes.push(arg);
    } else if (typeof arg === "number" && arg !== 0) {
      classes.push(String(arg));
    } else if (Array.isArray(arg)) {
      arg.forEach(processArg);
    } else if (typeof arg === "object" && arg !== null) {
      for (const key in arg) {
        if (Object.prototype.hasOwnProperty.call(arg, key) && arg[key]) {
          classes.push(key);
        }
      }
    }
  }

  args.forEach(processArg);

  return classes.join(" ");
}
```
