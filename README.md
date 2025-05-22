# LE JS c'est pas magic (un peu quand même 😜)  

---

# Comprendre ce qu’il se passe quand tu écris du JavaScript

---

## 1. JavaScript : le langage

* JavaScript est un **langage** défini par une norme appelée **ECMAScript**.
* Il contient des choses comme :

    * `String`, `Number`, `Object`, `console.log()`
    * `if`, `for`, `let`, `const`, `this`, etc.
* Mais… JavaScript **ne s’exécute pas tout seul** !

---

## 2. Le moteur JavaScript

* Pour **exécuter ton code JS**, un programme spécial est utilisé : un **moteur JavaScript**.
* Il est intégré dans :

    * Les **navigateurs** : Chrome → **V8**, Firefox → **SpiderMonkey**, Safari → **JavaScriptCore**
    * **Node.js** : utilise **V8**

---

## 3. V8 (le moteur de Chrome et Node.js)

* **V8 est écrit en C++** pour être **rapide et efficace**.
* Il lit ton code JavaScript et :

    1. **le décode (parse)**
    2. **le transforme en bytecode** (langage intermédiaire)
    3. **le compile en code machine** (que ton ordi peut exécuter)
* Il **ne transforme PAS ton JS en C++**.

---

## 4. Chaîne complète (vue simplifiée)

```text
Ton code JavaScript
↓
Le moteur V8 le lit
↓
Interprète / Compile en code machine
↓
Exécute sur ton ordinateur (navigateur ou Node.js)
↓
Affiche un résultat (dans la console, dans la page, etc.)
```

---

## 5. Exemple simple

```js
console.log("Bonjour !");
```

➡V8 va :

* Lire `console.log`
* Voir que `console` est un objet du navigateur
* Appeler sa méthode `log`, qui va afficher `"Bonjour !"`

---

## 6. Et le C++ dans tout ça ?

Le moteur V8 est **codé en C++** :

* Les objets comme `String`, `Array`, `Date` sont **programmés en C++**.
* Quand tu fais `new String("abc")`, c’est V8 qui appelle une fonction interne C++ pour créer un objet `String`.

Tu n’écris pas de C++, **mais il travaille en coulisses pour toi.**

---

## 7. Ce que tu manipules : des objets JS

```js
const nom = new String("Jean");
```

* C’est toi qui écris du JavaScript.
* V8 va construire **un objet `String`** en utilisant du code C++ interne.
* Il te retourne un **objet JS utilisable** dans ton code.

---

## 8. Résumé global

| Élément        | Rôle                           |
| -------------- | ------------------------------ |
| **JavaScript** | Le langage que tu écris        |
| **ECMAScript** | La norme officielle du langage |
| **V8**         | Le moteur qui exécute ton JS   |
| **C++**        | Langage utilisé pour coder V8  |

---


