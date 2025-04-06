# Promise.all

## Interview Question

Implémentez votre propre version de Promise.all(), une fonction promiseAll, à la différence que la fonction prend un tableau au lieu d'un itérable

## Description

**Promise.all()** est une méthode qui prend en entrée un itérable d'éléments (généralement des promesses) et renvoie une promesse unique qui se résout en un tableau des résultats des promesses d'entrée. Cette promesse renvoyée sera résolue lorsque toutes les promesses de l'entrée seront résolues, ou si l'itérable d'entrée ne contient aucune promesse. Elle rejette immédiatement toute erreur de promesse ou de non-promesse d'entrée, et rejettera avec ce premier message de rejet/erreur.

### Exemple

```js
const [userData, postsData, tagsData] = await Promise.all([
  fetch("/api/user"),
  fetch("/api/posts"),
  fetch("/api/tags"),
]);
```

## Interview Solution

```js
/**
 * @param {Array} iterable
 * @return {Promise<Array>}
 */
export default function promiseAll(iterable) {
  return new Promise((resolve, rejected) => {
    // On vérifie si le paramètre est un tableau
    if (!Array.isArray(iterable)) {
      return rejected("Argument  must be an array");
    }

    let results = []; // Tableau qui va contenir notre promesse résolue
    let resolvedCount = 0;
    const numPromises = iterable.length;

    // On vérifie si le tableau est vide
    if (numPromises === 0) {
      return resolve([]);
    }

    // On résous chaque promise du tableau
    iterable.forEach((promise, index) => {
      Promise.resolve(promise)
        .then((value) => {
          results[index] = value;
          resolvedCount++;

          if (resolvedCount === numPromises) {
            resolve(results);
          }
        })
        .catch(rejected);
    });
  });
}
```
