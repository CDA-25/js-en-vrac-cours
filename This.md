# Notre amis "THIS" en JavaScript

---

## Qu’est-ce que `this` ?

> `this` est une **référence dynamique** : sa valeur dépend **du contexte d’exécution**, ou dans le cas des fonctions fléchées, **du contexte d’écriture**.

---

## Deux grands types de fonctions :

| Type de fonction      | `this` est défini…               |
| --------------------- | -------------------------------- |
| `function` classique  | ... au **moment d’exécution**    |
| `=>` fonction fléchée | ... au **moment de déclaration** |

---

## 1. Fonction classique : `function`

```js
const user = {
  name: "Alice",
  hello: function () {
    console.log(this.name);
  }
};

user.hello(); // "Alice"
```

🔹 Ici, `this` est défini **au moment où `hello()` est appelée** → il vaut `user`.

---

## 2. Fonction fléchée : `=>`

```js
const user = {
  name: "Alice",
  hello: () => {
    console.log(this.name);
  }
};

user.hello(); // undefined
```

Cette fois, `this` **n’est pas `user`**. Pourquoi ?

---

### Explication essentielle :

> Les **fonctions fléchées ne créent pas leur propre `this`**.
> Elles **capturent** le `this` du contexte **où elles sont écrites**, **pas où elles sont appelées**.

---

### ⚠️ ⚠️ Important : **"où elles sont écrites" ≠ "où elles sont appelées"**

```js
// Contexte global
const user = {
  name: "Alice",
  hello: () => {
    console.log(this);       // ici `this` === globalThis (window ou undefined en strict)
  }
};

user.hello();
```

Même si tu appelles `hello()` **depuis `user`**, la fonction a été **écrite dans le contexte global**, donc `this` vient du **global**.

---

## Exemple contrasté avec fonction normale

```js
const user = {
  name: "Alice",
  hello() {
    console.log(this.name); // "Alice"
  }
};
```

➡Ici, `hello()` est une fonction **normale**, donc `this` est défini **au moment de l’appel**, et vaut `user`.

---

## Résumé clair :

| Fonction         | `this` pris depuis…                     | Résultat       |
| ---------------- | --------------------------------------- | -------------- |
| `function () {}` | Le contexte **au moment de l’appel**    | Dynamique      |
| `() => {}`       | Le contexte **au moment de l’écriture** | Lexical (fixe) |

---

## Exemple ultime : différence écriture / exécution

```js
function outer() {
  this.name = "outer";

  const arrow = () => {
    console.log("arrow this.name =", this.name);
  };

  function classic() {
    console.log("classic this.name =", this.name);
  }

  return { arrow, classic };
}

const obj = outer.call({ name: "customThis" });
obj.arrow();   // arrow this.name = customThis
obj.classic(); // classic this.name = undefined (appelée sans contexte)
```

➡`arrow` a capturé le `this` de `outer` au moment de l’écriture.
➡`classic` dépend du moment **d’exécution** — ici sans `call`, donc `this = undefined`.

---

## Dans un objet littéral

```js
const user = {
  name: "Alice",
  arrow: () => console.log(this.name),
  classic() {
    console.log(this.name);
  }
};

user.arrow();   // undefined
user.classic(); // "Alice"
```

Même si `arrow` est **écrite dans un objet**, son `this` **n’est pas** l’objet !
Elle est **déclarée** dans le **contexte global** (ou module), donc elle capture `this = undefined` ou `window`.

---

## Leçon à retenir

| Type de fonction | `this` capturé depuis...          | Quand l’utiliser             |
| ---------------- | --------------------------------- | ---------------------------- |
| `function()`     | Au moment de l’appel              | Méthodes, constructeurs      |
| `() => {}`       | Au moment de l’écriture (lexical) | Fonctions courtes, callbacks |

---

## Astuce mentale : pense en **"où elle est écrite"**

* Les fléchées **figent `this`** à l’endroit où tu les écris.
* Les classiques laissent `this` être **défini plus tard** au moment de l’appel.

---
