<p>
<a href="https://si3stael.github.io/tutos/starter">Démarrage</a> |
<a href="https://si3stael.github.io/tutos/tutorial">Tutoriel complet</a> |
<a href="https://si3stael.github.io/tutos/tutojava">Web Front-End</a> |
<a href="https://si3stael.github.io/tutos/api">L’API ChatGPT</a>
</p>

<hr>


# Tutoriel complet : Personnaliser votre galerie interactive avec IA

Bienvenue dans ce guide qui vous explique **pas à pas** comment personnaliser votre galerie interactive. Vous allez apprendre à créer vos propres scènes, définir le comportement de l'IA et gérer les transitions entre les œuvres.

---

## Table des matières

- [Tutoriel complet : Personnaliser votre galerie interactive avec IA](#tutoriel-complet--personnaliser-votre-galerie-interactive-avec-ia)
  - [Table des matières](#table-des-matières)
  - [Vue d'ensemble du projet](#vue-densemble-du-projet)
  - [Fichier 1 : `data.js` — Définir vos scènes](#fichier-1--datajs--définir-vos-scènes)
    - [Mot de passe](#mot-de-passe)
    - [Structure d'une scène](#structure-dune-scène)
    - [Champs à personnaliser](#champs-à-personnaliser)
      - [**`id`** — L'identifiant unique](#id--lidentifiant-unique)
      - [**`title`** — Le titre de l'œuvre](#title--le-titre-de-lœuvre)
      - [**`imageUrl`** — Le chemin de l'image](#imageurl--le-chemin-de-limage)
      - [**`temperature`** — La créativité de l'IA](#temperature--la-créativité-de-lia)
      - [**`firstUserMessage`** — Le message d'accueil](#firstusermessage--le-message-daccueil)
      - [**`systemPrompt`** — Le cerveau de l'IA](#systemprompt--le-cerveau-de-lia)
    - [Structure d'un bon systemPrompt](#structure-dun-bon-systemprompt)
    - [Exemple complet d'une scène](#exemple-complet-dune-scène)
    - [Système de transitions entre scènes](#système-de-transitions-entre-scènes)
    - [Ajouter une nouvelle scène](#ajouter-une-nouvelle-scène)
    - [Utiliser {{SCENES\_LIST}} (optionnel)](#utiliser-scenes_list-optionnel)
  - [Fichier 2 : `manip.js` — Gérer les commandes prédéterminées](#fichier-2--manipjs--gérer-les-commandes-prédéterminées)
    - [Rôle du fichier](#rôle-du-fichier)
    - [Structure de la fonction `beforeAI()`](#structure-de-la-fonction-beforeai)
    - [Commandes déjà implémentées](#commandes-déjà-implémentées)
      - [Commande "aide"](#commande-aide)
      - [Commande "nom"](#commande-nom)
      - [Commande "mon nom est X"](#commande-mon-nom-est-x)
      - [Commande "reset"](#commande-reset)
    - [Comment ajouter vos propres commandes](#comment-ajouter-vos-propres-commandes)
    - [Bonnes pratiques](#bonnes-pratiques)
  - [Fichier 3 : `prompt.js` — Personnaliser la construction du prompt](#fichier-3--promptjs--personnaliser-la-construction-du-prompt)
    - [Rôle du fichier](#rôle-du-fichier-1)
    - [Fonction actuelle](#fonction-actuelle)
    - [Ajouter vos propres transformations](#ajouter-vos-propres-transformations)
      - [Exemple 1 : Injecter le nom de l'utilisateur](#exemple-1--injecter-le-nom-de-lutilisateur)
      - [Exemple 2 : Injecter la date actuelle](#exemple-2--injecter-la-date-actuelle)
      - [Exemple 3 : Contexte selon le numéro de scène](#exemple-3--contexte-selon-le-numéro-de-scène)
  - [Fichier 4 : `promptVars.js` — Gérer les variables globales pour les prompts](#fichier-4--promptvarsjs--gérer-les-variables-globales-pour-les-prompts)
    - [Rôle du fichier](#rôle-du-fichier-2)
    - [Structure actuelle](#structure-actuelle)
    - [Comment ça fonctionne ?](#comment-ça-fonctionne-)
    - [Ajouter vos propres variables](#ajouter-vos-propres-variables)
    - [Modifier les variables dynamiquement](#modifier-les-variables-dynamiquement)
    - [Bonnes pratiques](#bonnes-pratiques-1)
  - [Récapitulatif des fichiers](#récapitulatif-des-fichiers)
  - [Workflow complet : Ajouter une nouvelle œuvre](#workflow-complet--ajouter-une-nouvelle-œuvre)
    - [Étape 1 : Préparer votre image](#étape-1--préparer-votre-image)
    - [Étape 2 : Créer la scène dans `data.js`](#étape-2--créer-la-scène-dans-datajs)
    - [Étape 3 : Mettre à jour la scène précédente](#étape-3--mettre-à-jour-la-scène-précédente)
    - [Étape 4 : (Optionnel) Ajouter une commande spéciale](#étape-4--optionnel-ajouter-une-commande-spéciale)
    - [Étape 5 : Tester !](#étape-5--tester-)
  - [Débogage courant](#débogage-courant)
    - [Problème 1 : La scène ne s'affiche pas](#problème-1--la-scène-ne-saffiche-pas)
    - [Problème 2 : La transition ne fonctionne pas](#problème-2--la-transition-ne-fonctionne-pas)
    - [Problème 3 : L'IA ne suit pas les instructions](#problème-3--lia-ne-suit-pas-les-instructions)
    - [Problème 4 : Ma commande dans `manip.js` ne marche pas](#problème-4--ma-commande-dans-manipjs-ne-marche-pas)
  - [Exemples de prompts pour différents styles](#exemples-de-prompts-pour-différents-styles)
    - [Style pédagogique classique](#style-pédagogique-classique)
    - [Style ludique et engageant](#style-ludique-et-engageant)
    - [Style mystérieux et immersif](#style-mystérieux-et-immersif)
    - [Style scientifique et analytique](#style-scientifique-et-analytique)
  - [✅ Checklist avant de soumettre votre projet](#-checklist-avant-de-soumettre-votre-projet)
  - [Conseils finaux](#conseils-finaux)
    - [Pour de bons `systemPrompt`](#pour-de-bons-systemprompt)
    - [Pour de bonnes commandes](#pour-de-bonnes-commandes)
    - [Pour une bonne expérience](#pour-une-bonne-expérience)
  - [Besoin d'aide ?](#besoin-daide-)
  - [Questions fréquentes](#questions-fréquentes)

---

## Vue d'ensemble du projet

Votre projet se compose de plusieurs fichiers JavaScript. Vous allez principalement modifier **quatre fichiers** :

| Fichier | Rôle | Ce que vous devez faire |
|---------|------|------------------------|
| `data.js` | Contient les données de vos scènes | Définir vos œuvres, images, et le comportement de l'IA pour chaque scène |
| `manip.js` | Gère les commandes prédéterminées | Ajouter des commandes spéciales (aide, reset, etc.) |
| `prompt.js` | Construit le prompt système | Personnaliser la manière dont le contexte est envoyé à l'IA |
| `promptVars.js` | Gère les variables globales pour les prompts | Définir des variables à utiliser dans les prompts |

> ⚠️ **Important** : Vous ne devez **PAS** modifier `app.js` qui gère la communication avec l'API et l'interface.

---

## Fichier 1 : `data.js` — Définir vos scènes

### Mot de passe

C'est dans le fichier data.js que vous allez entrer le mot de passe pour accéder à l'API OpenAI (les appels à l'API ne sont pas un service gratuit et sont facturés). Vous devrez remplacer la valeur de la variable `password` par le mot de passe spécifique de votre groupe, que vous trouverez sur moodle:

La ligne 3 devient donc :

```javascript
const password = "gXXXXXXXXXX";
```

Attention à ne pas partager ce mot de passe en dehors de votre groupe. Ce mot de passe est nécessaire pour que l'application puisse communiquer avec l'API OpenAI, nous pouvons ainsi suivre l'utilisation de l'API par chaque groupe et compter les crédits utilisés afin de nous assurer que vous n'utilisez pas l'API de manière abusive.

### Structure d'une scène

Chaque scène dans le tableau `scenes` représente une œuvre d'art. Voici tous les champs que vous pouvez utiliser :

```javascript
{
  id: "scene-art-02",                    // Identifiant unique de la scène
  title: "Impression, soleil levant",    // Titre affiché dans l'interface
  imageUrl: "assets/img/02-monnet.jpeg", // Chemin vers l'image
  chatHistory: [],                       // Historique de conversation (ne pas modifier)
  temperature: 0.3,                      // Créativité de l'IA (0.0 = précis, 1.0 = créatif)
  firstUserMessage: "Bonjour, peux-tu m'aider ?", // Premier message automatique
  systemPrompt: `...`                    // Instructions pour l'IA (voir ci-dessous)
}
```

### Champs à personnaliser

#### **`id`** — L'identifiant unique

```javascript
id: "scene-art-02"
```

- Doit être **unique** pour chaque scène
- Utilisé pour les transitions (`GOTO:scene-art-03`)
- Convention : `scene-art-XX` ou `scene-XXX`

#### **`title`** — Le titre de l'œuvre

```javascript
title: "Impression, soleil levant"
```

- Affiché dans l'interface utilisateur
- Doit être court et descriptif

#### **`imageUrl`** — Le chemin de l'image

```javascript
imageUrl: "assets/img/02-monnet.jpeg"
```

- Chemin relatif vers votre image
- Formats supportés : `.jpg`, `.jpeg`, `.png`, `.webp`

#### **`temperature`** — La créativité de l'IA

```javascript
temperature: 0.3
```

- Valeur entre `0.0` et `1.0`
- `0.0` → Réponses très précises et cohérentes
- `0.5` → Équilibre entre précision et créativité
- `1.0` → Réponses très créatives et variées
- **Conseil** : Gardez `0.3` pour un guide pédagogique stable

**Exemples pratiques :**

```javascript
temperature: 0.0   // Réponses très prévisibles, toujours similaires
                   // → Bon pour : questions factuelles, définitions

temperature: 0.3   // Légèrement créatif tout en restant cohérent
                   // → Bon pour : guides pédagogiques (RECOMMANDÉ)

temperature: 0.7   // Plus de variété dans les réponses
                   // → Bon pour : discussions créatives

temperature: 1.0   // Maximum de créativité, parfois surprenant
                   // → Bon pour : poésie, histoires, brainstorming
```

**Pour votre projet :** Gardez `0.3` sauf si vous voulez un guide très poétique (0.5-0.7).

#### **`firstUserMessage`** — Le message d'accueil

```javascript
firstUserMessage: "Bonjour, peux-tu m'aider ?"
```

- Premier message envoyé automatiquement par "l'utilisateur" à l'IA
- Lance la conversation quand on arrive sur la scène
- Peut être personnalisé selon le contexte

#### **`systemPrompt`** — Le cerveau de l'IA

C'est **le plus important** ! Le `systemPrompt` définit le rôle, le comportement et les objectifs de l'IA pour cette scène.

### Structure d'un bon systemPrompt

```javascript
systemPrompt: `
  Tu es un guide [PERSONNALITÉ], spécialiste de [DOMAINE].
  
  Tu accompagnes l'utilisateur dans l'observation de [ŒUVRE].
  
  Règles de comportement :
  - [Règle 1]
  - [Règle 2]
  - [Règle 3]
  
  Objectif pédagogique :
  [Ce que l'utilisateur doit comprendre]
  
  Gestion de la progression :
  - Après **le deuxième message de l'utilisateur**, tu dois conclure
  - Si l'utilisateur comprend plus vite, tu conclus immédiatement
  - La conclusion doit être claire, brève (4-6 phrases)
  
  Déclenchement de la scène suivante :
  - Lorsque l'utilisateur tape le mot-clé exact « [MOT-CLÉ] »
    **ou** lorsque tu conclus pédagogiquement,
    tu termines ton message en incluant exactement :
    <!-- GOTO:[ID-SCENE-SUIVANTE] -->
  - Tu indiques explicitement que l'œuvre suivante a été débloquée.
`
```

### Exemple complet d'une scène

```javascript
{
  id: "scene-van-gogh",
  title: "La Nuit étoilée",
  imageUrl: "assets/img/van-gogh-nuit-etoilee.jpg",
  chatHistory: [],
  temperature: 0.3,
  firstUserMessage: "Bonjour, que vois-tu dans ce tableau ?",
  systemPrompt: `
    Tu es un guide passionné et enthousiaste, spécialiste de l'art post-impressionniste.
    
    Tu accompagnes l'utilisateur dans l'observation de 
    « La Nuit étoilée » de Vincent van Gogh (1889).
    
    Règles de comportement :
    - Tu encourages l'observation des mouvements et des tourbillons
    - Tu poses des questions sur les émotions ressenties
    - Tu évites le jargon technique au début
    - Tu guides vers l'expression des sentiments plutôt que l'analyse froide
    
    Objectif pédagogique :
    Faire comprendre que van Gogh exprime ses émotions intérieures 
    à travers le mouvement et la couleur, pas une simple représentation du ciel.
    
    Gestion de la progression :
    - Après **le deuxième message de l'utilisateur**, tu dois conclure
    - Si l'utilisateur comprend plus vite, tu conclus immédiatement
    - La conclusion doit être claire, brève (4-6 phrases)
    
    Déclenchement de la scène suivante :
    - Lorsque l'utilisateur tape le mot-clé exact « émotion »
      **ou** lorsque tu conclus pédagogiquement,
      tu termines ton message en incluant exactement :
      <!-- GOTO:scene-monet -->
    - Tu indiques explicitement que l'œuvre suivante a été débloquée.
  `
}
```

###  Système de transitions entre scènes

Les transitions se font via un **marqueur spécial** que l'IA inclut dans sa réponse :

```html
<!-- GOTO:scene-art-03 -->
```

**Comment ça marche ?**

1. Dans votre `systemPrompt`, vous demandez à l'IA d'inclure ce marqueur
2. Vous définissez **quand** l'IA doit l'inclure :
   - Quand l'utilisateur tape un **mot-clé** spécifique
   - Quand l'IA a **terminé son objectif pédagogique**
3. Quand l'IA inclut ce marqueur, `app.js` détecte automatiquement et charge la scène suivante

**Exemple pratique (à inclure dans le systemPrompt) :**

```javascript
Déclenchement de la scène suivante :
- Lorsque l'utilisateur tape le mot-clé exact « structure »
  **ou** lorsque tu conclus pédagogiquement,
  tu termines ton message en incluant exactement :
  <!-- GOTO:scene-art-03 -->
- Tu indiques explicitement que l'œuvre suivante a été débloquée.
```



### Ajouter une nouvelle scène

**Étape 1** : Copiez une scène existante

```javascript
const scenes = [
  { /* scène existante 1 */ },
  { /* scène existante 2 */ },
  // Ajoutez votre nouvelle scène ici :
  {
    id: "scene-ma-nouvelle-oeuvre",
    title: "Ma nouvelle œuvre",
    imageUrl: "assets/img/ma-nouvelle-image.jpg",
    chatHistory: [],
    temperature: 0.3,
    firstUserMessage: "Bonjour !",
    systemPrompt: `...`
  }
];
```

**Étape 2** : Modifiez les valeurs selon votre œuvre

**Étape 3** : Mettez à jour le marqueur `GOTO` de la scène précédente pour pointer vers votre nouvelle scène

### Utiliser `{% raw %}{{SCENES_LIST}}{% endraw %}` (optionnel)

Si vous voulez que l'IA connaisse **toutes les scènes disponibles**, vous pouvez écrire dans votre `systemPrompt` :
{% raw %}
```javascript
systemPrompt: `
  Voici les scènes disponibles dans cette galerie :
  {{SCENES_LIST}}
  
  Tu peux mentionner ces œuvres dans tes explications...
`
```
{% endraw %}
La fonction `buildSystemPromptForScene()` remplacera automatiquement `{% raw %}{{SCENES_LIST}}{% endraw %}` par :

```
- scene-art-02 — Impression, soleil levant
- scene-art-03 — Mont Sainte-Victoire
- scene-art-04 — Portrait d'Ambroise Vollard
```

---

## Fichier 2 : `manip.js` — Gérer les commandes prédéterminées

### Rôle du fichier

`manip.js` contient la fonction `beforeAI()` qui **intercepte** les messages de l'utilisateur **avant** qu'ils soient envoyés à l'IA.

**Pourquoi ?**
- Pour gérer des **commandes spéciales** (aide, reset, nom, etc.)
- Pour éviter de solliciter l'IA pour des tâches simples
- Pour avoir un contrôle total sur certaines interactions

### Structure de la fonction `beforeAI()`

```javascript
function beforeAI(userText, scene){
    let laisseAIdecider = true;
    
    // Vos conditions ici
    
    return laisseAIdecider;
}
```

**Paramètres :**

- `userText` : Le texte tapé par l'utilisateur
- `scene` : L'objet scène actuel (contient `id`, `title`, etc.)

**Retour :**

- `true` → L'IA sera appelée pour répondre
- `false` → La commande a été gérée, pas besoin de l'IA

### Commandes déjà implémentées

#### Commande "aide"

```javascript
if(userText.toLowerCase() === "aide"){
    msg = `Voici un peu d'aide.\n
Écris "aide" pour afficher ce menu d'aide.\n
Écris "rep [mot-clé]" pour débloquer une nouvelle scène.\n
Écris "nom" pour que je te rappelle ton nom.\n
Écris "reset" pour revenir à la première scène.`
    addMessageToUI("assistant", msg);
    laisseAIdecider = false;  // ← Pas besoin de l'IA
}
```

#### Commande "nom"

```javascript
else if(userText.toLowerCase() === "nom"){
    msg = "Tu t'appelles " + promptVars.userName + ".";
    msg += `\n\nSi tu veux changer de nom
écris "mon nom est X", en écrivant ton nom à la place de X.`;
    addMessageToUI("assistant", msg);
    laisseAIdecider = false;
}
```

#### Commande "mon nom est X"

```javascript
else if(userText.toLowerCase().startsWith("mon nom est ")){
    const newName = userText.substring("mon nom est ".length).trim();
    promptVars.userName = newName;// Mise à jour dans promptVars
    msg = "Tu t'appelles dorénavant " + promptVars.userName;
    msg += "\nCe nom sera utilisé dans toutes les scènes.";
    addMessageToUI("assistant", msg);
    laisseAIdecider = false;
}
```

#### Commande "reset"

```javascript
else if(userText.toLowerCase() === "reset"){
    selectScene(0);  // Retourne à la première scène
    return false;
}
```

### Comment ajouter vos propres commandes

**Exemple 1 : Commande "indice"**

```javascript
else if(userText.toLowerCase() === "indice"){
    msg = `Indice : Observe attentivement les couleurs et les formes...`;
    addMessageToUI("assistant", msg);
    laisseAIdecider = false;
}
```

**Exemple 2 : Commande "sauter" pour passer à la scène suivante**

```javascript
else if(userText.toLowerCase() === "sauter"){
    // Trouver l'index de la scène actuelle
    const currentIndex = scenes.findIndex(s => s.id === scene.id);
    if(currentIndex < scenes.length - 1){
        selectScene(currentIndex + 1);
        msg = "Passage à la scène suivante...";
        addMessageToUI("assistant", msg);
    } else {
        msg = "Vous êtes déjà à la dernière scène !";
        addMessageToUI("assistant", msg);
    }
    laisseAIdecider = false;
}
```

**Exemple 3 : Commande contextuelle (selon la scène)**

```javascript
// À la fin de la fonction, AVANT le return
if(scene.id === "scene-van-gogh" && userText.toLowerCase().includes("folie")){
    msg = `\n\n Note historique : Van Gogh a effectivement souffert de troubles mentaux, 
mais cela ne diminue en rien son génie artistique.`;
    addMessageToUI("assistant", msg);
    // On garde laisseAIdecider = true pour que l'IA réponde aussi
}
```

### Bonnes pratiques

✅ **À faire :**

- Utilisez `.toLowerCase()` pour ignorer la casse
- Retournez `false` quand vous gérez complètement la commande
- Utilisez `else if` pour éviter de vérifier toutes les conditions

❌ **À éviter :**

- Ne gérez pas tout avec des commandes (laissez l'IA faire son travail)
- N'oubliez pas le `return` à la fin
- Ne modifiez pas directement `chatHistory` (laissez `app.js` s'en charger)

---

## Fichier 3 : `prompt.js` — Personnaliser la construction du prompt

### Rôle du fichier

`prompt.js` contient la fonction `buildSystemPromptForScene()` qui **transforme** le `systemPrompt` d'une scène avant de l'envoyer à l'IA.

### Fonction actuelle

{% raw %}
```javascript
function buildSystemPromptForScene(scene){
  let p = (scene.systemPrompt || "").trim();
  p = replaceTemplates(p);

  // Option pratique : si tu veux injecter une liste des scènes dans le prompt
  // en écrivant {{SCENES_LIST}} dans systemPrompt
  if (p.includes("{{SCENES_LIST}}")) {
    const list = scenes.map(s => `- ${s.id} — ${s.title}`).join("\n");
    p = p.replaceAll("{{SCENES_LIST}}", list);
  }

  return p;
}
```
{% endraw %}

**Comment ça fonctionne :**

1. **Ligne 2** : Récupère le `systemPrompt` de la scène
2. **Ligne 3** : `replaceTemplates(p)` remplace automatiquement **toutes les variables** de `promptVars.js`
   - Par exemple : `{% raw %}{{userName}}{% endraw %}` devient `"Alice"` et `{% raw %}{{age}}{% endraw %}` devient `15`
3. **Lignes 5-9** : Si le prompt contient `{% raw %}{{SCENES_LIST}}{% endraw %}`, il est remplacé par la liste de toutes les scènes
4. **Ligne 11** : Retourne le prompt transformé

**Différence entre `promptVars` et `{{SCENES_LIST}}` :**

| Type | Défini dans | Exemple | Usage |
|------|-------------|---------|-------|
| **Variables promptVars** | `promptVars.js` | `{% raw %}{{userName}}{% endraw %}`, `{% raw %}{{age}}{% endraw %}` | Informations utilisateur réutilisables partout |
| **Variables spéciales** | `prompt.js` | `{% raw %}{{SCENES_LIST}}{% endraw %}` | Informations calculées dynamiquement |


### Ajouter vos propres transformations

#### Exemple 1 : Injecter la date actuelle

{% raw %}
```javascript
function buildSystemPromptForScene(scene){
  let p = (scene.systemPrompt || "").trim();
  p = replaceTemplates(p);

  if (p.includes("{{SCENES_LIST}}")) {
    const list = scenes.map(s => `- ${s.id} — ${s.title}`).join("\n");
    p = p.replaceAll("{{SCENES_LIST}}", list);
  }

  // Injecter la date du jour
  if (p.includes("{{TODAY}}")) {
    const today = new Date().toLocaleDateString('fr-FR');
    p = p.replaceAll("{{TODAY}}", today);
  }

  return p;
}
```
{% endraw %}

**Utilisation dans `data.js` :**
```javascript
systemPrompt: `
  Aujourd'hui nous sommes le {{TODAY}}.
  Tu accompagnes {{userName}} ({{age}} ans) dans l'observation de cette œuvre...
`
```

**Résultat final envoyé à l'IA :**
```
Aujourd'hui nous sommes le 11/02/2026.
Tu accompagnes Alice (15 ans) dans l'observation de cette œuvre...
```


#### Exemple 2 : Contexte selon le numéro de scène

{% raw %}
```javascript
function buildSystemPromptForScene(scene){
  let p = (scene.systemPrompt || "").trim();
  p = replaceTemplates(p);

  if (p.includes("{{SCENES_LIST}}")) {
    const list = scenes.map(s => `- ${s.id} — ${s.title}`).join("\n");
    p = p.replaceAll("{{SCENES_LIST}}", list);
  }

  // Ajouter un contexte selon la position dans la galerie
  const sceneIndex = scenes.findIndex(s => s.id === scene.id);
  if(sceneIndex === 0){
    p += "\n\nNote : C'est la première œuvre de la visite. Sois accueillant.";
  } else if(sceneIndex === scenes.length - 1){
    p += "\n\nNote : C'est la dernière œuvre. Propose une synthèse de la visite.";
  }

  return p;
}
```
{% endraw %}

**Note importante :** Les variables de `promptVars.js` (`{% raw %}{{userName}}{% endraw %}`, `{% raw %}{{age}}{% endraw %}`, etc.) sont **automatiquement** remplacées par `replaceTemplates(p)` à la ligne 3. Vous n'avez **pas besoin** de les gérer manuellement dans cette fonction.

> 📖 **Pour en savoir plus** : Consultez la section [Fichier 4 : `promptVars.js`](#fichier-4--promptvarsjs--gérer-les-variables-globales-pour-les-prompts) pour apprendre à définir vos propres variables.

---

## Fichier 4 : `promptVars.js` — Gérer les variables globales pour les prompts

### Rôle du fichier

`promptVars.js` crée un espace global de variables qui permettent de **personnaliser dynamiquement** les prompts système. Au lieu de réécrire manuellement les prompts pour chaque utilisateur, vous définissez une fois vos variables et les injectez où vous voulez.

### Structure actuelle

```javascript
window.promptVars = {
  userName: "Alice",  // Nom du joueur
  age: 15            // Âge du joueur
};
```

### Comment ça fonctionne ?

**Étape 1** : Vous définissez vos variables dans `promptVars.js`

**Étape 2** : Vous les utilisez dans vos prompts avec la syntaxe `{% raw %}{{nomVariable}}{% endraw %}`

{% raw %}
```javascript
systemPrompt: `
  Tu accompagnes l'utilisateur nommé {{userName}}, âgé de {age}} ans...
`
```
{% endraw %}


**Étape 3** : La fonction `replaceTemplates()` (dans `utils.js`) remplace automatiquement `{% raw %}{{userName}}{% endraw %}` par `"Alice"` et `{% raw %}{{age}}{% endraw %}` par `15` avant d'envoyer le prompt à l'IA.

### Ajouter vos propres variables

```javascript
window.promptVars = {
  userName: "Alice",
  age: 15,
  niveau: "débutant",           // Nouveau
  interet: "impressionnisme",   // Nouveau
  langue: "français"            // Nouveau
};
```

**Utilisation dans `data.js` :**

{% raw %}
```javascript
systemPrompt: `
  Tu t'adresses à {{userName}}, un visiteur {{niveau}} de {{age}} ans, 
  particulièrement intéressé par {{interet}}.
  Tu t'exprimes en {{langue}}.
`
```
{% endraw %}

### Modifier les variables dynamiquement

Dans `manip.js`, vous pouvez changer les valeurs pendant l'exécution :

```javascript
else if(userText.toLowerCase().startsWith("mon age est ")){
    const newAge = parseInt(userText.substring("mon age est ".length).trim());
    promptVars.age = newAge;  // Modification de la variable
    msg = "Tu as maintenant " + promptVars.age + " ans dans le système.";
    addMessageToUI("assistant", msg);
    laisseAIdecider = false;
}
```

### Bonnes pratiques

✅ **À faire :**

- Utilisez des noms de variables clairs (`userName` plutôt que `n`)
- Regroupez les variables liées (informations utilisateur ensemble)
- Documentez chaque variable avec un commentaire

❌ **À éviter :**

- Ne mettez pas de données sensibles dans ce fichier
- N'utilisez pas d'espaces dans les noms de variables

---

## Récapitulatif des fichiers

| Action | Fichier | Méthode |
|--------|---------|---------|
| Ajouter une œuvre | `data.js` | Ajouter un objet dans `scenes[]` |
| Définir le comportement de l'IA | `data.js` | Modifier le `systemPrompt` |
| Changer le mot-clé de transition | `data.js` | Modifier la section "Déclenchement" du `systemPrompt` |
| Ajouter une commande spéciale | `manip.js` | Ajouter un `else if` dans `beforeAI()` |
| Créer des transformations avancées de prompts | `prompt.js` | Ajouter des remplacements dans `buildSystemPromptForScene()` |
| Définir des variables globales réutilisables | `promptVars.js` | Ajouter des propriétés dans `window.promptVars` |

---

## Workflow complet : Ajouter une nouvelle œuvre

### Étape 1 : Préparer votre image

1. Placez votre image dans `assets/img/`
2. Nommez-la clairement (ex: `05-dali-persistence.jpg`)

### Étape 2 : Créer la scène dans `data.js`

```javascript
const scenes = [
  // ... scènes existantes ...
  {
    id: "scene-art-05",
    title: "La Persistance de la mémoire",
    imageUrl: "assets/img/05-dali-persistence.jpg",
    chatHistory: [],
    temperature: 0.4,  // Un peu plus créatif pour Dalí
    firstUserMessage: "Bonjour, ce tableau me perturbe...",
    systemPrompt: `
      Tu es un guide énigmatique et poétique, spécialiste du surréalisme.
      
      Tu accompagnes l'utilisateur dans l'observation de 
      « La Persistance de la mémoire » de Salvador Dalí (1931).
      
      Règles de comportement :
      - Tu encourages l'acceptation de l'étrangeté et du rêve
      - Tu poses des questions sur les sensations d'absurdité
      - Tu valorises l'imagination et l'inconscient
      - Tu évites les explications rationnelles trop rapides
      
      Objectif pédagogique :
      Faire comprendre que le surréalisme explore l'inconscient et 
      les rêves, en défiant la logique du monde réel.
      
      Gestion de la progression :
      - Après **le deuxième message de l'utilisateur**, tu dois conclure
      - La conclusion doit être claire, brève (4-6 phrases)
      
      Déclenchement de la scène suivante :
      - Lorsque l'utilisateur tape le mot-clé exact « rêve »
        **ou** lorsque tu conclus pédagogiquement,
        tu termines ton message en incluant exactement :
        <!-- GOTO:scene-art-06 -->
      - Tu indiques explicitement que l'œuvre suivante a été débloquée.
    `
  }
];
```

### Étape 3 : Mettre à jour la scène précédente

Dans la scène `scene-art-04`, changez le `GOTO` :

```javascript

<!-- GOTO:scene-art-05 -->  // Au lieu de scene-art-04 ou rien

```

### Étape 4 : (Optionnel) Ajouter une commande spéciale

Dans `manip.js`, ajoutez par exemple :

```javascript
else if(userText.toLowerCase() === "dali" && scene.id === "scene-art-05"){
    msg = `🎨 Salvador Dalí (1904-1989) était connu pour sa moustache 
extravagante et son excentricité, autant que pour son génie artistique !`;
    addMessageToUI("assistant", msg);
    laisseAIdecider = false;
}
```

### Étape 5 : Tester !

1. Ouvrez `index.html` dans votre navigateur
2. Naviguez jusqu'à votre nouvelle scène
3. Testez l'interaction avec l'IA
4. Vérifiez que la transition fonctionne

---

## Débogage courant

### Problème 1 : La scène ne s'affiche pas

**Solution :**
- Vérifiez que l'`id` est unique
- Vérifiez que le chemin `imageUrl` est correct
- Ouvrez la console du navigateur (F12) pour voir les erreurs

### Problème 2 : La transition ne fonctionne pas

**Solution :**
- Vérifiez que le marqueur `<!-- GOTO:scene-XXX -->` est exactement comme ça
- Vérifiez que l'`id` cible existe dans `scenes[]`
- Vérifiez que le `systemPrompt` demande bien à l'IA d'inclure ce marqueur

### Problème 3 : L'IA ne suit pas les instructions

**Solution :**

- Soyez plus **explicite** dans le `systemPrompt`
- Utilisez des **exemples** de ce que vous attendez
- Baissez la `temperature` pour plus de cohérence
- Relisez votre prompt : est-il clair et non ambigu ?

### Problème 4 : Ma commande dans `manip.js` ne marche pas

**Solution :**

- Vérifiez que vous utilisez `userText.toLowerCase()` pour la comparaison
- Vérifiez que vous retournez bien `false` si vous gérez la commande
- Vérifiez qu'il n'y a pas de `return` prématuré avant votre condition

---

## Exemples de prompts pour différents styles

### Style pédagogique classique

```javascript
systemPrompt: `
  Tu es un professeur d'histoire de l'art expérimenté.
  
  Tu utilises la méthode socratique : tu poses des questions 
  pour amener l'élève à découvrir par lui-même.
  
  Tu es patient, encourageant et structuré dans tes explications.
`
```

### Style ludique et engageant

```javascript
systemPrompt: `
  Tu es un guide enthousiaste et passionné, comme un animateur de musée 
  qui adore partager son amour de l'art.
  
  Tu utilises des métaphores, des comparaisons et des anecdotes 
  pour rendre l'art accessible et amusant.
  
  Tu n'hésites pas à utiliser des émojis pour dynamiser tes réponses. 🎨
`
```

### Style mystérieux et immersif

```javascript
systemPrompt: `
  Tu es un personnage mystérieux qui semble connaître les secrets 
  cachés derrière chaque œuvre.
  
  Tu parles de manière poétique et énigmatique, en laissant 
  planer le mystère sans tout révéler d'un coup.
  
  Tu poses des questions qui invitent à la contemplation profonde.
`
```

### Style scientifique et analytique

```javascript
systemPrompt: `
  Tu es un conservateur de musée spécialiste en analyse technique des œuvres.
  
  Tu t'intéresses aux techniques picturales, aux pigments utilisés, 
  à la composition géométrique et au contexte historique précis.
  
  Tu restes accessible mais tu n'hésites pas à utiliser le vocabulaire 
  technique approprié quand c'est nécessaire.
`
```

---
<!-- 
## 🎓 Exercices pratiques

### Exercice 1 : Créer une nouvelle scène
1. Choisissez une œuvre d'art qui vous plaît
2. Trouvez une image de cette œuvre
3. Créez une nouvelle scène complète dans `data.js`
4. Définissez un objectif pédagogique clair
5. Choisissez un mot-clé de transition approprié

### Exercice 2 : Ajouter une commande "citation"
1. Dans `manip.js`, ajoutez une commande `citation`
2. Cette commande doit afficher une citation célèbre sur l'art
3. La citation peut changer selon la scène actuelle

### Exercice 3 : Créer un parcours thématique
1. Créez 3 scènes sur un thème commun (ex: "Portraits", "Paysages", "Art abstrait")
2. Assurez-vous que les transitions sont cohérentes
3. Ajoutez une synthèse finale dans la dernière scène

### Exercice 4 : Variable dynamique personnalisée
1. Dans `prompt.js`, créez une variable `{{MOOD}}`
2. Cette variable doit refléter le "ton" de la scène (joyeux, mélancolique, etc.)
3. Utilisez-la dans vos `systemPrompt`

---
-->

## ✅ Checklist avant de soumettre votre projet

- [ ] Toutes mes scènes ont un `id` unique
- [ ] Toutes mes images sont présentes dans `assets/img/`
- [ ] Chaque `systemPrompt` définit clairement l'objectif pédagogique
- [ ] Les transitions entre scènes fonctionnent (marqueurs `GOTO`)
- [ ] J'ai testé toutes mes commandes personnalisées dans `manip.js`
- [ ] Mon code est indenté et lisible
- [ ] J'ai commenté les parties complexes de mon code
- [ ] J'ai vérifié qu'il n'y a pas d'erreurs dans la console (F12)
- [ ] L'expérience utilisateur est fluide et agréable

---

##  Conseils finaux

### Pour de bons `systemPrompt`

1. **Soyez spécifique** : "Tu poses des questions sur les couleurs" plutôt que "Tu es sympa"
2. **Donnez des exemples** : Montrez à l'IA le type de réponse que vous voulez
3. **Limitez la longueur** : 2-3 échanges max par scène pour garder le rythme
4. **Testez et ajustez** : Le prompt engineering est itératif !

### Pour de bonnes commandes

1. **Simplicité** : Commandes courtes et mémorables ("aide", "indice", "reset")
2. **Cohérence** : Gardez le même style de commandes partout
3. **Documentation** : Affichez les commandes disponibles avec "aide"

### Pour une bonne expérience

1. **Progressivité** : Commencez simple, complexifiez progressivement
2. **Feedback** : L'utilisateur doit toujours savoir ce qui se passe
3. **Clarté** : Les transitions doivent être évidentes et fluides

---

<!-- 
## Ressources complémentaires

- [Documentation de l'API Chatgpt](https://openai.com/api/)
- [Guide du prompt engineering](https://help.openai.com/en/articles/10032626-prompt-engineering-best-practices-for-chatgpt)
- [Markdown guide](https://www.markdownguide.org/) (pour formater les réponses de l'IA)
---
-->


## Besoin d'aide ?

Si vous rencontrez un problème :

1. **Vérifiez la console** (F12 dans le navigateur)
2. **Relisez ce guide** (la réponse est souvent là !)
3. **Testez par petits morceaux** (isolez le problème)
4. **Demandez à votre professeur** avec un exemple précis du problème


---

## Questions fréquentes

**Q : Le mot de passe ne fonctionne pas, que faire ?**
→ Vérifiez que vous avez bien copié le mot de passe complet depuis Moodle, avec les guillemets. Si le problème persiste, contactez votre enseignant.

**Q : L'IA ne répond plus, que se passe-t-il ?**
→ Vérifiez la console (F12) pour voir s'il y a des erreurs. Cela peut être dû à un quota dépassé ou à une erreur dans votre code.

<!--
**Q : Comment savoir combien de crédits mon groupe a utilisés ?**
→ Consultez le tableau de suivi sur Moodle qui est mis à jour régulièrement.

**Q : Puis-je tester mon code sans utiliser de crédits ?**
→ Oui ! Vous pouvez tester toutes les commandes dans `manip.js` (aide, nom, reset, etc.) sans appeler l'IA. Seules les réponses générées par l'IA consomment des crédits.
--->

**Q : La transition ne se déclenche pas, pourquoi ?**
→ Vérifiez que l'IA inclut bien `<!-- GOTO:scene-XXX -->` dans sa réponse. Vous pouvez le voir dans la console ou dans le panneau de debug.

**Q : Comment voir ce qui est envoyé à l'IA ?**
→ Cliquez sur le bouton "Debug" dans l'interface pour voir le JSON envoyé et reçu.

---

**Bonne création !**

N'oubliez pas : l'art et la programmation ont beaucoup en commun — ce sont tous deux des formes de créativité qui demandent de la patience, de la pratique et de l'expérimentation. Ne vous découragez pas si tout ne marche pas du premier coup !
