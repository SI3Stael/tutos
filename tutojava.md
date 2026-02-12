<p>
<a href="https://si3stael.github.io/tutos/starter">Démarrage</a> |
<a href="https://si3stael.github.io/tutos/tutorial">Tutoriel complet</a> |
<a href="https://si3stael.github.io/tutos/tutojava">Web Front-End</a> |
<a href="https://si3stael.github.io/tutos/api">L’API ChatGPT</a>
</p>

<hr>


# Tutoriel : Développement Web Front-End

Bienvenue dans ce guide qui vous explique les bases du développement web front-end, de la création de pages HTML à l'utilisation de JavaScript pour rendre vos sites interactifs.

- [Tutoriel : Développement Web Front-End](#tutoriel--développement-web-front-end)
  - [Introduction : Qu'est-ce que le Front-End ?](#introduction--quest-ce-que-le-front-end-)
  - [Partie 1 : HTML — La structure de votre page](#partie-1--html--la-structure-de-votre-page)
    - [Qu'est-ce que le HTML ?](#quest-ce-que-le-html-)
    - [Structure de base d'un fichier HTML](#structure-de-base-dun-fichier-html)
    - [Les balises HTML essentielles](#les-balises-html-essentielles)
    - [Exemple complet](#exemple-complet)
  - [Partie 2 : CSS — Le style de votre page](#partie-2--css--le-style-de-votre-page)
  - [Partie 3 : JavaScript — L'interactivité de votre page](#partie-3--javascript--linteractivité-de-votre-page)
    - [Qu'est-ce que JavaScript ?](#quest-ce-que-javascript-)
    - [Lier JavaScript à HTML](#lier-javascript-à-html)
      - [1. JavaScript dans la balise `<script>` (dans le HTML)](#1-javascript-dans-la-balise-script-dans-le-html)
      - [2. JavaScript dans un fichier externe (recommandé)](#2-javascript-dans-un-fichier-externe-recommandé)
    - [Ordre de chargement important](#ordre-de-chargement-important)
    - [📌 Dans votre projet](#-dans-votre-projet)
  - [Partie 4 : JavaScript — Les bases du langage](#partie-4--javascript--les-bases-du-langage)
    - [Les variables](#les-variables)
      - [Déclaration de variables](#déclaration-de-variables)
      - [Types de données essentiels](#types-de-données-essentiels)
    - [Les structures conditionnelles (if/else)](#les-structures-conditionnelles-ifelse)
      - [Structure de base](#structure-de-base)
      - [Opérateurs de comparaison](#opérateurs-de-comparaison)
      - [Opérateurs logiques](#opérateurs-logiques)
      - [Exemples pratiques](#exemples-pratiques)
    - [Les fonctions](#les-fonctions)
      - [Déclaration de fonction classique](#déclaration-de-fonction-classique)
      - [Fonction avec paramètres](#fonction-avec-paramètres)
      - [Fonction avec valeur de retour](#fonction-avec-valeur-de-retour)
    - [📌 Dans votre projet](#-dans-votre-projet-1)
      - [Exemple concret du projet](#exemple-concret-du-projet)
  - [Partie 5 : Déboguer avec la console — Les bases](#partie-5--déboguer-avec-la-console--les-bases)
    - [Ouvrir les outils de développement](#ouvrir-les-outils-de-développement)
    - [Les onglets principaux](#les-onglets-principaux)
    - [Utiliser `console.log()` pour déboguer](#utiliser-consolelog-pour-déboguer)
      - [Syntaxe de base](#syntaxe-de-base)
      - [Afficher plusieurs valeurs](#afficher-plusieurs-valeurs)
    - [Inspecter les erreurs](#inspecter-les-erreurs)
    - [En résumé](#en-résumé)
  - [Partie 6 : Ressources pour aller plus loin](#partie-6--ressources-pour-aller-plus-loin)
  - [Conclusion](#conclusion)
  - [Questions fréquentes](#questions-fréquentes)

---

## Introduction : Qu'est-ce que le Front-End ?

Le **développement front-end** concerne tout ce que l'utilisateur voit et avec lequel il interagit dans un navigateur web.

**Les trois piliers du front-end :**

| Technologie | Rôle | Analogie |
|-------------|------|----------|
| **HTML** | Structure et contenu | Le squelette d'une maison |
| **CSS** | Apparence et style | La décoration et la peinture |
| **JavaScript** | Interactivité et logique | L'électricité et la plomberie |

---

## Partie 1 : HTML — La structure de votre page

### Qu'est-ce que le HTML ?

**HTML** (HyperText Markup Language) est le langage qui définit la **structure** et le **contenu** de votre page web.

Dans votre projet, vous allez lancer votre page web en ouvrant le fichier `index.html` dans un navigateur (Edge, Chrome, Firefox, etc.). Ce fichier est écrit en HTML.

### Structure de base d'un fichier HTML

```html
<!DOCTYPE html>
<html lang="fr">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Ma première page</title>
</head>
<body>
  <h1>Bonjour le monde !</h1>
  <p>Ceci est ma première page web.</p>
</body>
</html>
```

**Explication des balises :**

- `<!DOCTYPE html>` : Indique au navigateur qu'il s'agit d'un document HTML5
- `<html>` : Balise racine qui contient tout le document
- `<head>` : Contient les métadonnées (titre, liens CSS, etc.)
- `<body>` : Contient le contenu visible de la page

### Les balises HTML essentielles

```html
<!-- Titres (h1 = plus important, h6 = moins important) -->
<h1>Titre principal</h1>
<h2>Sous-titre</h2>
<h3>Sous-sous-titre</h3>

<!-- Paragraphe -->
<p>Ceci est un paragraphe de texte.</p>

<!-- Lien -->
<a href="https://www.exemple.com">Cliquez ici</a>

<!-- Image -->
<img src="mon-image.jpg" alt="Description de l'image">

<!-- Bouton -->
<button>Cliquez-moi</button>

<!-- Zone de texte -->
<input type="text" placeholder="Entrez votre nom">

<!-- Division (conteneur) -->
<div>
  <p>Contenu regroupé dans une division</p>
</div>

<!-- Liste non ordonnée -->
<ul>
  <li>Élément 1</li>
  <li>Élément 2</li>
  <li>Élément 3</li>
</ul>
```
<!-- Liste ordonnée 
<ol>
  <li>Premier</li>
  <li>Deuxième</li>
  <li>Troisième</li>
</ol>
-->

### Exemple complet

```html
<!DOCTYPE html>
<html lang="fr">
<head>
  <meta charset="UTF-8">
  <title>Mon Portfolio</title>
</head>
<body>
  <h1>Bienvenue sur mon site</h1>
  
  <h2>À propos de moi</h2>
  <p>Je m'appelle Alice et j'apprends le développement web.</p>
  
  <h2>Mes projets</h2>
  <ul>
    <li>Site personnel</li>
    <li>Galerie d'art interactive</li>
    <li>Application de to-do list</li>
  </ul>
  
  <button>Contactez-moi</button>
</body>
</html>
```

Vous pouvez copier ce code dans un fichier `.html` et l'ouvrir dans votre navigateur pour voir le résultat.

---

## Partie 2 : CSS — Le style de votre page

C'est le CSS qui rend votre page jolie et agréable à utiliser. Si vous êtes intéressé par le design web, le CSS est votre meilleur allié ! Mais dans notre projet, nous ne vous demanderons pas de changer l'apparence visuelle du site web donc nous n'allons pas présenter le CSS en détail. Sachez juste que si vous voyez dans le fichier HTML des liens vers des fichiers `.css`, c'est pour appliquer du style à la page.

Dans votre projet, le fichier `styles.css` contient déjà tous les styles nécessaires. Vous n'aurez pas besoin de le modifier, mais vous pouvez le consulter si vous êtes curieux de voir comment les éléments sont stylisés !

Passons maintenant à JavaScript, qui est **le cœur de votre projet**.

---

## Partie 3 : JavaScript — L'interactivité de votre page

### Qu'est-ce que JavaScript ?

**JavaScript** est le langage de programmation qui permet d'ajouter de l'**interactivité** à vos pages web (réagir aux clics, modifier le contenu, communiquer avec des serveurs, communiquer avec l'API chatgpt, etc.).

### Lier JavaScript à HTML

Il existe deux façons principales d'inclure du code JavaScript dans une page HTML :

#### 1. JavaScript dans la balise `<script>` (dans le HTML)

```html
<body>
  <button id="monBouton">Cliquez-moi</button>
  
  <script>
    document.getElementById('monBouton').onclick = function() {
      alert('Bonjour !');
    };
  </script>
</body>
```

⚠️ **Acceptable** pour de petits scripts

#### 2. JavaScript dans un fichier externe (recommandé)

**index.html :**

```html
<body>
  <button id="monBouton">Cliquez-moi</button>
  
  <!-- Fichier JS à la fin du body -->
  <script src="script.js"></script>
</body>
```

**script.js :**

```javascript
document.getElementById('monBouton').onclick = function() {
  alert('Bonjour !');
};
```

Ce petit code affichera une alerte "Bonjour !" lorsque l'utilisateur cliquera sur le bouton. Le code JavaScript est placé dans un fichier séparé `script.js` et lié à la page HTML via la balise `<script>`. Le bouton est créé dans le HTML avec un identifiant `monBouton`, ce qui permet au script de le sélectionner et d'ajouter un gestionnaire d'événement pour le clic.

✅ **Recommandé** : code organisé et réutilisable

### Ordre de chargement important

⚠️ **Le JavaScript doit être chargé APRÈS les éléments HTML qu'il manipule !**

```html
<!-- ❌ MAUVAIS : le bouton n'existe pas encore -->
<head>
  <script src="script.js"></script>
</head>
<body>
  <button id="monBouton">Cliquez-moi</button>
</body>

<!-- ✅ BON : le bouton existe déjà -->
<body>
  <button id="monBouton">Cliquez-moi</button>
  <script src="script.js"></script>
</body>
```

### 📌 Dans votre projet

Vous allez principalement travailler dans les fichiers JavaScript :

- `manip.js` — Gère les commandes prédéterminées
- `data.js` — Définit les scènes et les prompts
- `prompt.js` — Construit les prompts système

Tous ces fichiers sont déjà liés à `index.html` via des balises `<script>` à la fin du `<body>`.

---

## Partie 4 : JavaScript — Les bases du langage

### Les variables

#### Déclaration de variables

```javascript
// let : variable qui peut changer
let age = 25;
age = 26;  // OK

// const : variable qui ne peut PAS changer (constante)
const nom = "Alice";
// nom = "Bob";  // ❌ ERREUR !
```

**Règle d'or :** Utilisez `const` par défaut, `let` si la valeur doit changer.

#### Types de données essentiels

En JavaScript, les variables peuvent contenir différents types de valeurs :

```javascript
// Nombres
let age = 25;
let prix = 19.99;

// Texte (chaînes de caractères)
let nom = "Alice";
let message = 'Bonjour';

// Booléens (vrai/faux)
let estMajeur = true;
let estConnecte = false;

// Tableaux (listes)
let couleurs = ["rouge", "vert", "bleu"];

// Objets (données structurées)
let personne = {
  nom: "Alice",
  age: 25
};
```

**Astuce :** Vous pouvez toujours vérifier le type d'une variable avec `typeof` :

```javascript
console.log(typeof age);  // "number"
console.log(typeof nom);  // "string"
```


### Les structures conditionnelles (if/else)

#### Structure de base

```javascript
let age = 18;

if (age >= 18) {
  console.log("Vous êtes majeur");
} else {
  console.log("Vous êtes mineur");
}
```

#### Opérateurs de comparaison

```javascript
let x = 10;

// Égalité
x == 10    // true  (égalité de valeur, éviter)
x === 10   // true  (égalité stricte, recommandé)
x === "10" // false (types différents)

// Inégalité
x != 5     // true
x !== "10" // true  (recommandé)

// Comparaisons
x > 5      // true  (supérieur)
x >= 10    // true  (supérieur ou égal)
x < 20     // true  (inférieur)
x <= 10    // true  (inférieur ou égal)
```

#### Opérateurs logiques

```javascript
let age = 25;
let permis = true;

// ET (&&) : toutes les conditions doivent être vraies
if (age >= 18 && permis) {
  console.log("Vous pouvez conduire");
}

// OU (||) : au moins une condition doit être vraie
if (age < 18 || !permis) {
  console.log("Vous ne pouvez pas conduire");
}

// NON (!) : inverse la condition
if (!permis) {
  console.log("Vous n'avez pas le permis");
}
```

#### Exemples pratiques

```javascript
// If / else if / else
let note = 15;

if (note >= 16) {
  console.log("Très bien");
} else if (note >= 14) {
  console.log("Bien");
} else if (note >= 12) {
  console.log("Assez bien");
} else if (note >= 10) {
  console.log("Passable");
} else {
  console.log("Insuffisant");
}

// Conditions imbriquées
let age = 20;
let nationalite = "française";

if (age >= 18) {
  if (nationalite === "française") {
    console.log("Vous pouvez voter en France");
  } else {
    console.log("Vous êtes majeur mais pas français");
  }
} else {
  console.log("Vous êtes mineur");
}

// Opérateur ternaire (condition courte)
let statut = age >= 18 ? "majeur" : "mineur";
console.log(statut);  // "majeur"
```

### Les fonctions

#### Déclaration de fonction classique

```javascript
// Fonction sans paramètre ni retour
function direBonjour() {
  console.log("Bonjour !");
}

// Appel de la fonction
direBonjour();  // Affiche "Bonjour !"
```

#### Fonction avec paramètres

```javascript
function direBonjour(nom) {
  console.log("Bonjour " + nom + " !");
}

direBonjour("Alice");  // "Bonjour Alice !"
direBonjour("Bob");    // "Bonjour Bob !"

// Plusieurs paramètres
function addition(a, b) {
  let resultat = a + b;
  console.log(resultat);
}

addition(5, 3);  // 8
```

#### Fonction avec valeur de retour

```javascript
function addition(a, b) {
  return a + b;
}

let resultat = addition(5, 3);
console.log(resultat);  // 8

// Utilisation directe
console.log(addition(10, 20));  // 30

// Exemple plus complexe
function estMajeur(age) {
  if (age >= 18) {
    return true;
  } else {
    return false;
  }
}

// Version simplifiée
function estMajeur(age) {
  return age >= 18;
}

if (estMajeur(20)) {
  console.log("Accès autorisé");
}
```

### 📌 Dans votre projet

Vous utiliserez souvent :
- **Variables** : `promptVars.userName`, `scenes`, `chatHistory`
- **Conditions** : pour gérer les commandes dans `manip.js`
- **Fonctions** : `beforeAI()`, `buildSystemPromptForScene()`, etc.
  
#### Exemple concret du projet

Voici une fonction simple qu'on pourrait ajouter dans `manip.js` :

```javascript
// Fonction pour vérifier si l'utilisateur est un adulte
function estAdulte(age) {
  return age >= 18;
}

// Utilisation dans beforeAI
if (userText === "age") {
  if (estAdulte(promptVars.age)) {
    msg = "Tu es adulte, bienvenue !";
  } else {
    msg = "Tu es mineur, contenu adapté.";
  }
  addMessageToUI("assistant", msg);
  laisseAIdecider = false;
}
```

Ce type de fonction vous permet de **réutiliser** la même logique à plusieurs endroits.

---

## Partie 5 : Déboguer avec la console — Les bases

### Ouvrir les outils de développement

**Raccourcis clavier :**
- **Windows/Linux** : `F12` ou `Ctrl + Shift + I`
- **Mac** : `Cmd + Option + I`

**Ou via le menu :**
- Chrome : Menu (⋮) → Plus d'outils → Outils de développement
- Firefox : Menu (☰) → Développement web → Outils de développement

### Les onglets principaux

| Onglet | Utilité |
|--------|---------|
| **Elements** (ou Inspecteur) | Voir et modifier le HTML et CSS en temps réel |
| **Console** | Voir les logs, erreurs, et exécuter du JavaScript |
| **Sources** (ou Débogueur) | Déboguer le code JavaScript ligne par ligne |
| **Network** (ou Réseau) | Voir les requêtes réseau (images, API, etc.) |

### Utiliser `console.log()` pour déboguer

#### Syntaxe de base

```javascript
// Afficher un message simple
console.log("Début du script");

// Afficher une variable
let age = 25;
console.log(age);

// Afficher avec un label
console.log("L'âge est :", age);
```

#### Afficher plusieurs valeurs

```javascript
let nom = "Alice";
let age = 25;
let ville = "Paris";

// Plusieurs valeurs séparées par des virgules
console.log("Nom:", nom, "Age:", age, "Ville:", ville);

// Avec template literal (plus lisible)
console.log(`Nom: ${nom}, Age: ${age}, Ville: ${ville}`);
```

### Inspecter les erreurs

Quand une erreur se produit, la console affiche :

```
Uncaught ReferenceError: maVariable is not defined
    at script.js:15
```

**Informations fournies :**

- **Type d'erreur** : `ReferenceError`
- **Message** : `maVariable is not defined`
- **Fichier et ligne** : `script.js:15`

**Cliquez sur le lien** pour aller directement à la ligne problématique !

### En résumé

Pour déboguer efficacement votre code :

1. **Ouvrez la console** avec F12
2. **Utilisez `console.log()`** pour afficher des valeurs
3. **Lisez les messages d'erreur** pour trouver les bugs
4. **Testez régulièrement** votre code au fur et à mesure

💡 **Astuce :** Prenez l'habitude d'ouvrir la console dès que vous travaillez sur votre projet !

---

## Partie 6 : Ressources pour aller plus loin

**Documentation officielle :**

- [MDN Web Docs](https://developer.mozilla.org/fr/) — La référence pour HTML, CSS, JavaScript
- [W3Schools](https://www.w3schools.com/) — Tutoriels et exemples pratiques

**Apprendre JavaScript :**

- [JavaScript.info](https://javascript.info/) — Cours complet et moderne
- [Eloquent JavaScript](https://eloquentjavascript.net/) — Livre gratuit en ligne

**Pratiquer :**

- [freeCodeCamp](https://www.freecodecamp.org/) — Exercices interactifs gratuits
- [Codecademy](https://www.codecademy.com/) — Cours interactifs

**Outils utiles :**

- [CodePen](https://codepen.io/) — Tester du code HTML/CSS/JS en ligne
- [JSFiddle](https://jsfiddle.net/) — Idem
- [Visual Studio Code](https://code.visualstudio.com/) — Éditeur de code recommandé

---
<!--
## Conclusion

Vous avez maintenant les bases du développement web front-end !

**Ce que vous savez faire :**
- ✅ Créer la structure d'une page avec HTML
- ✅ Styliser une page avec CSS
- ✅ Ajouter de l'interactivité avec JavaScript
- ✅ Manipuler le DOM (Document Object Model)
- ✅ Déboguer votre code avec F12 et la console
- ✅ Créer un projet complet fonctionnel

**Prochaines étapes :**
1. **Pratiquez** : créez vos propres projets
2. **Explorez** : découvrez les frameworks (React, Vue, etc.)
3. **Approfondissez** : apprenez ES6+, async/await, APIs
4. **Partagez** : mettez vos projets en ligne (GitHub Pages, Netlify)
--->

## Conclusion

Vous avez maintenant les connaissances de base pour comprendre et modifier votre projet de galerie interactive !

**Ce que vous maîtrisez :**

- ✅ La structure HTML de base
- ✅ Le rôle du JavaScript dans l'interactivité
- ✅ Les variables, conditions et fonctions
- ✅ L'utilisation de la console pour déboguer

**Pour votre projet spécifique :**

1. **Commencez par lire** le code existant pour comprendre la structure
2. **Utilisez `console.log()`** pour voir ce qui se passe
3. **Testez vos modifications** une par une
4. **Consultez ce tutoriel** quand vous avez un doute

**N'oubliez pas :** Chaque développeur, même expérimenté, consulte régulièrement la documentation et fait des erreurs. C'est normal et ça fait partie de l'apprentissage !

---

## Questions fréquentes

**Q : J'ai modifié mon code mais rien ne change dans le navigateur ?**  
→ Rechargez la page avec `Ctrl + F5` (Windows) ou `Cmd + Shift + R` (Mac).

**Q : J'ai une erreur "Cannot read property of null" ?**  
→ Vérifiez que l'ID de l'élément HTML existe et est correctement orthographié.

**Q : Comment savoir si mon JavaScript est chargé ?**  
→ Ajoutez `console.log("Script chargé !")` au début de votre fichier JS et vérifiez dans la console.

**Q : Où trouver de l'aide sur mon projet spécifique ?**  
→ Consultez le tutoriel de personnalisation de la galerie qui explique `data.js`, `manip.js` et `prompt.js`.


**Bon développement ! 🚀**


