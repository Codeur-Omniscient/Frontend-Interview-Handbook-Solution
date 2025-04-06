# Debounce

## Interview Question

Implémentez une fonction debounce qui accepte une fonction de rappel et une durée d'attente. L'appel de debounce() renvoie une fonction qui a neutralisé les appels de la fonction de rappel, conformément au comportement décrit ci-dessus.

## Définition

Debounce est une **Technique** Javascript permet de gérer des évènement qui se déclenche fréquemment. Il permet donc de **Limiter** la fréquence d'exécution d'une fonction en attendant qu'un certain délai se soit écoulé sans que l'événement en question ne se produise à nouveau

## Interview Solution

```js
export default function debounce(func, wait) {
  let timeoutId;

  return function (...args) {
    clearTimeout(timeoutId); // Annule le minuteur précédent si un nouvel événement se produit
    timeoutId = setTimeout(() => {
      func.apply(this, args); // Exécute la fonction après le délai
    }, wait);
  };
}
```
