# Event Emitter

## Interview Question

Dans le **Observer Pattern** (aussi appelé **Publish-Subscribe** model), nous pouvons observer/s'abonner aux événements émis par les éditeurs et exécuter du code dès qu'un événement se produit.
Implémentez une classe **EventEmitter** similaire à celle de Node.js qui suit ce modèle d'observation.

## Description

Un EventEmitter est un modèle de conception (souvent implémenté comme une classe dans les langages de programmation) qui permet à un objet (l'émetteur) de notifier d'autres objets (les auditeurs ou observateurs) lorsqu'un événement spécifique se produit. Il suit le modèle de l'observateur (Observer pattern).

### Exemple

```js
const emitter = new EventEmitter();

function addTwoNumbers(a, b) {
  console.log(`The sum is ${a + b}`);
}
emitter.on("foo", addTwoNumbers);
emitter.emit("foo", 2, 5);
// > "The sum is 7"

emitter.on("foo", (a, b) => console.log(`The product is ${a * b}`));
emitter.emit("foo", 4, 5);
// > "The sum is 9"
// > "The product is 20"

emitter.off("foo", addTwoNumbers);
emitter.emit("foo", -3, 9);
// > "The product is -27"
```

## Interview Solution

```js
export default class EventEmitter {
  constructor() {
    this._events = {}; // Stocke les auditeurs par nom d'événement.
  }

  /**
   * Ajoute un auditeur pour un événement.
   * @param {string} eventName - Nom de l'événement.
   * @param {Function} listener - Fonction à exécuter.
   * @returns {this}
   */
  on(eventName, listener) {
    if (!this._events[eventName]) {
      this._events[eventName] = []; // Initialise le tableau si nécessaire.
    }
    this._events[eventName].push(listener); // Ajoute l'auditeur.
    return this;
  }

  /**
   * Supprime un auditeur pour un événement (première occurrence).
   * @param {string} eventName - Nom de l'événement.
   * @param {Function} listenerToRemove - Auditeur à supprimer.
   * @returns {this}
   */
  off(eventName, listenerToRemove) {
    if (this._events[eventName]) {
      const index = this._events[eventName].indexOf(listenerToRemove);
      if (index !== -1) {
        this._events[eventName].splice(index, 1); // Supprime l'auditeur trouvé.
      }
      if (this._events[eventName].length === 0) {
        delete this._events[eventName]; // Nettoie si plus d'auditeurs.
      }
    }
    return this;
  }

  /**
   * Émet un événement et appelle ses auditeurs.
   * @param {string} eventName - Nom de l'événement à émettre.
   * @param {...any} args - Arguments passés aux auditeurs.
   * @returns {boolean} - True si des auditeurs ont été appelés.
   */
  emit(eventName, ...args) {
    const listeners = this._events[eventName];
    if (listeners && Array.isArray(listeners)) {
      listeners.forEach((listener) => listener.apply(this, args)); // Appelle chaque auditeur.
      return true;
    }
    return false;
  }
}
```
