# Deep Clone

## Interview Question

Implémentez une fonction deepClone qui effectue un clonage profond sur des objets JavaScript. L'entrée ne contient que des valeurs sérialisables en JSON (null, boolean, number, string, Array, Object) et ne contiendra aucun autre objet comme Date, Regex, Map or Set.

## Description

Un deep clone (ou clonage profond) est le processus de création d'une copie exacte d'un objet (ou d'un tableau), y compris tous ses objets et tableaux imbriqués, de manière à ce que la copie soit complètement indépendante de l'original. Modifier la copie n'affectera en aucun cas l'objet original, et inversement.

### Exemple

```js
const obj1 = { user: { role: "admin" } };
const clonedObj1 = deepClone(obj1);

clonedObj1.user.role = "guest"; // Change the cloned user's role to 'guest'.
clonedObj1.user.role; // 'guest'
obj1.user.role; // Should still be 'admin'.

const obj2 = { foo: [{ bar: "baz" }] };
const clonedObj2 = deepClone(obj2);

obj2.foo[0].bar = "bax"; // Modify the original object.
obj2.foo[0].bar; // 'bax'
clonedObj2.foo[0].bar; // Should still be 'baz'.
```

## Interview Solution

```js
/**
 * @template T
 * @param {T} value
 * @return {T}
 */
export default function deepClone(value) {
  // Sérialise l'objet en une chaîne JSON
  const jsonString = JSON.stringify(value);
  // Désérialise la chaîne JSON pour créer une nouvelle instance de l'objet
  return JSON.parse(jsonString);
}
```
