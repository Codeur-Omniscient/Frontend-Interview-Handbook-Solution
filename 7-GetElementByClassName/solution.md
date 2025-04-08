# GetElementByClassName

## Interview Question

Implémentons notre propre fonction Element.getElementsByClassName(), similaire mais légèrement différente :

Il s'agit d'une fonction pure qui prend un élément et une chaîne classNames, contenant un ou plusieurs noms de classe à rechercher, séparés par des espaces. Par exemple : getElementsByClassName(document.body, 'foo bar').
Similaire à Element.getElementsByClassName(), seuls les descendants de l'argument élément sont recherchés, et non l'élément lui-même.
Renvoie un tableau d'éléments, au lieu d'une collection HTML d'éléments.
N'utilisez pas document.querySelectorAll(), car cela rendrait le problème trivial. Vous ne serez pas autorisé à l'utiliser lors d'entretiens réels.

## Description

getElementsByClassName() est une méthode qui existe sur les documents et éléments HTML pour renvoyer une HTMLCollection d'éléments descendants dans le document/élément qui a le(s) nom(s) de classe spécifié(s).

### Exemple

```js
const doc = new DOMParser().parseFromString(
  `<div class="foo bar baz">
    <span class="bar baz">Span</span>
    <p class="foo baz">Paragraph</p>
    <div class="foo bar"></div>
  </div>`,
  "text/html"
);

getElementsByClassName(doc.body, "foo bar");
// [div.foo.bar.baz, div.foo.bar] <-- This is an array of elements.
```

## Interview Solution

```js
/**
 * @param {Element} element
 * @param {string} classNames
 * @return {Array<Element>}
 */
export default function getElementsByClassName(element, classNames) {
  const result = [];
  const targetClasses = classNames.trim().split(/\s+/);

  function deepSearch(node) {
    // On ignore le noeud racine, seulement ses descendants comptent
    for (let child of node.children) {
      const elementClasses = child.classList;
      const hasAllClasses = targetClasses.every((cls) =>
        elementClasses.contains(cls)
      );
      if (hasAllClasses) {
        result.push(child);
      }
      // Recurse sur les enfants
      deepSearch(child);
    }
  }

  deepSearch(element);
  return result;
}
```
