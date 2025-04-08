# Array.prototype.filter

## Interview Question

Étant donné un tableau d'entiers arr et une fonction de filtrage fn, renvoie un tableau filtré, filteredArr.

La fonction fn prend un ou deux arguments :

arr[i] - nombre du tableau
i - index de arr[i]
filteredArr ne doit contenir que les éléments du tableau pour lesquels l'expression fn(arr[i], i) est évaluée comme vraie. Une valeur vraie est une valeur pour laquelle Boolean(value) renvoie vrai.

Veuillez résoudre ce problème sans la méthode Array.filter intégrée.

### Exemple

```javascript

Input: arr = [0,10,20,30], fn = function greaterThan10(n) { return n > 10; }
Output: [20,30]
Explanation:
const newArray = filter(arr, fn); // [20, 30]
The function filters out values that are not greater than 10
```

## Interview Solution

```js
/**
 * @param {number[]} arr
 * @param {Function} fn
 * @return {number[]}
 */
export default function filter(arr, fn) {
  let filteredArr = [];
  for (i = 0; i < arr.length; i++) {
    let value = fn(arr[i], i);
    if (Boolean(value) === true) {
      filteredArr.push(arr[i]);
    }
  }

  return filteredArr;
}
```
