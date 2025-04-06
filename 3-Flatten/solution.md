# Flatten

## Interview Question

Implémenter une fonction flatten qui renvoie un tableau nouvellement créé avec tous les éléments du sous-tableau concaténés de manière récursive en un seul niveau

## Description

Une fonction **flatten** est une fonction qui prend en entrée un tableau potentiellement multidimensionnel (c'est-à-dire un tableau contenant d'autres tableaux comme éléments) et renvoie un nouveau tableau à une seule dimension contenant tous les éléments des sous-tableaux, concaténés de manière récursive

### Exemple

```js
// Single-level arrays are unaffected.
flatten([1, 2, 3]); // [1, 2, 3]

// Inner arrays are flattened into a single level.
flatten([1, [2, 3]]); // [1, 2, 3]
flatten([
  [1, 2],
  [3, 4],
]); // [1, 2, 3, 4]

// Flattens recursively.
flatten([1, [2, [3, [4, [5]]]]]); // [1, 2, 3, 4, 5]
```

## Interview Solution

```js
/**
 * @param {Array<*|Array>} value
 * @return {Array}
 */
export default function flatten(value) {
  const flattened = [];

  for (let i = 0; i < value.length; i++) {
    if (Array.isArray(value[i])) {
      // Si l'élément est un tableau, la fonction flatten s'appelle récursivement et concatène le résultat
      flattened.push(...flatten(value[i]));
    } else {
      // Si l'élément n'est pas un tableau, il est automatiquement ajouter au tableau flattened
      flattened.push(value[i]);
    }
  }

  return flattened;
}
```
