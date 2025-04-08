# List Format

## Interview Question

Étant donné une liste de chaînes, implémentez une fonction listFormat qui renvoie les éléments concaténés en une seule chaîne. Un cas d'utilisation courant serait la synthèse des réactions aux publications sur les réseaux sociaux.

La fonction doit prendre en charge plusieurs options comme deuxième paramètre :

sorted : trie les éléments par ordre alphabétique.
length : affiche uniquement les premiers éléments de longueur, en utilisant « and X other(s) » pour les autres. Ignore les valeurs non valides (négatives, 0, etc.).
unique : supprime les doublons.

### Example

```js
listFormat([]); // ''

listFormat(["Bob"]); // 'Bob'
listFormat(["Bob", "Alice"]); // 'Bob and Alice'

listFormat(["Bob", "Ben", "Tim", "Jane", "John"]);
// 'Bob, Ben, Tim, Jane and John'

listFormat(["Bob", "Ben", "Tim", "Jane", "John"], {
  length: 3,
}); // 'Bob, Ben, Tim and 2 others'

listFormat(["Bob", "Ben", "Tim", "Jane", "John"], {
  length: 4,
}); // 'Bob, Ben, Tim, Jane and 1 other'

listFormat(["Bob", "Ben", "Tim", "Jane", "John"], {
  length: 3,
  sorted: true,
}); // 'Ben, Bob, Jane and 2 others'

listFormat(["Bob", "Ben", "Tim", "Jane", "John", "Bob"], {
  length: 3,
  unique: true,
}); // 'Bob, Ben, Tim and 2 others'

listFormat(["Bob", "Ben", "Tim", "Jane", "John"], {
  length: 3,
  unique: true,
}); // 'Bob, Ben, Tim and 2 others'

listFormat(["Bob", "Ben", "", "", "John"]); // 'Bob, Ben and John'
```

## Interview Solution

```js
export default function listeFormat(elements = [], options = {}) {
  // Vérification des cas limites
  if (!elements || elements.length === 0) return "";

  // Traitement des éléments
  let listeTraitee = [...elements].filter((el) => el !== "");

  // Déduplication si demandée
  if (options.unique) {
    listeTraitee = Array.from(new Set(listeTraitee));
  }

  // Tri si demandé
  if (options.sorted) {
    listeTraitee.sort();
  }

  // Vérification après filtrage
  if (listeTraitee.length === 0) return "";
  if (listeTraitee.length === 1) return listeTraitee[0];

  // Application de la limite si spécifiée
  const limite = parseInt(options.length, 10);
  const limiteValide =
    !isNaN(limite) && limite > 0 && limite < listeTraitee.length;

  if (limiteValide) {
    const elementsVisibles = listeTraitee.slice(0, limite);
    const nombreRestants = listeTraitee.length - limite;

    return `${elementsVisibles.join(", ")} and ${nombreRestants} ${
      nombreRestants === 1 ? "other" : "others"
    }`;
  }

  // Cas standard (tous les éléments affichés)
  if (listeTraitee.length === 2) {
    return `${listeTraitee[0]} and ${listeTraitee[1]}`;
  }

  const dernierElement = listeTraitee.pop();
  return `${listeTraitee.join(", ")} and ${dernierElement}`;
}
```
