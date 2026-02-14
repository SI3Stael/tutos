<p>
<a href="https://si3stael.github.io/tutos/starter">Démarrage</a> |
<a href="https://si3stael.github.io/tutos/tutorial">Tutoriel complet</a> |
<a href="https://si3stael.github.io/tutos/tutojs">Web Front-End</a> |
<a href="https://si3stael.github.io/tutos/api">L’API ChatGPT</a>
</p>

<hr>


# Guide de démarrage rapide : Galerie interactive avec IA

Bienvenue ! Ce guide vous accompagne dans vos **premiers pas** avec le projet de galerie interactive. Pour des explications détaillées, consultez le [tutoriel complet](tutorial).

---

## Table des matières

- [Guide de démarrage rapide : Galerie interactive avec IA](#guide-de-démarrage-rapide--galerie-interactive-avec-ia)
  - [Table des matières](#table-des-matières)
  - [Étape 1 : Télécharger et installer le projet](#étape-1--télécharger-et-installer-le-projet)
  - [Étape 2 : Configurer votre mot de passe API](#étape-2--configurer-votre-mot-de-passe-api)
  - [Étape 3 : Découvrir l'interface](#étape-3--découvrir-linterface)
    - [Ouvrir le projet](#ouvrir-le-projet)
    - [Explorer l'interface](#explorer-linterface)
    - [Utiliser le panneau Debug](#utiliser-le-panneau-debug)
  - [Étape 4 : Comprendre le rôle du compagnon IA](#étape-4--comprendre-le-rôle-du-compagnon-ia)
    - [Qu'est-ce que le compagnon IA ?](#quest-ce-que-le-compagnon-ia-)
    - [Comment fonctionne-t-il ?](#comment-fonctionne-t-il-)
    - [Testez les exemples fournis](#testez-les-exemples-fournis)
  - [Étape 5 : Planifier votre projet](#étape-5--planifier-votre-projet)
    - [Réfléchissez à vos scènes](#réfléchissez-à-vos-scènes)
    - [Définissez le rôle du compagnon](#définissez-le-rôle-du-compagnon)
    - [Exercice de planification](#-exercice-de-planification)
  - [Étape 6 : Modifier les scènes existantes](#étape-6--modifier-les-scènes-existantes)
    - [Pourquoi commencer par modifier ?](#pourquoi-commencer-par-modifier-)
    - [Première modification : Changer le titre](#première-modification--changer-le-titre)
    - [Deuxième modification : Adapter le systemPrompt](#deuxième-modification--adapter-le-systemprompt)
    - [Testez vos modifications](#testez-vos-modifications)
  - [Étape 7 : Utiliser la console (F12) pour déboguer](#étape-7--utiliser-la-console-f12-pour-déboguer)
    - [Ouvrir la console](#ouvrir-la-console)
    - [Que voir dans la console ?](#que-voir-dans-la-console-)
    - [Utiliser console.log() dans votre code](#utiliser-consolelog-dans-votre-code)
    - [Comprendre les erreurs](#comprendre-les-erreurs)
  - [Prochaines étapes](#prochaines-étapes)
  - [Ressources](#ressources)
  - [Besoin d'aide ?](#besoin-daide-)

---

## Étape 1 : Télécharger et installer le projet

1. **Téléchargez le fichier ZIP** depuis Moodle
2. **Décompressez** le fichier dans un dossier de votre choix
3. **Vérifiez** que vous avez cette structure de fichiers :

```
galerie-interactive/
│
├── index.html          ← Page principale
├── styles.css          ← Styles visuels
│
├── assets/
│   └── img/            ← Images des œuvres
│
├── data.js             ← Définition des scènes
├── manip.js            ← Commandes personnalisées
├── prompt.js           ← Construction des prompts
├── promptVars.js       ← Variables globales
├── utils.js            ← Fonctions utilitaires
└── app.js              ← Logique principale (NE PAS MODIFIER)
```

> ⚠️ **Important** : Ne modifiez **jamais** le fichier `app.js` !

---

## Étape 2 : Configurer votre mot de passe API

**Pourquoi ?** L'application utilise l'API OpenAI (ChatGPT) pour générer les réponses du compagnon IA. Chaque groupe a un mot de passe unique qui nous permet de suivre votre consommation de [tokens](api#9-tokens).

**Comment faire :**

1. Ouvrez le fichier `data.js` avec un éditeur de texte (Notepad++, VS Code, etc.)
2. Trouvez la ligne 3 :
   ```javascript
   const password = "g01XXXXXX";
   ```
3. Remplacez `"g01XXXXXX"` par **votre mot de passe de groupe** (disponible sur Moodle)
4. **Sauvegardez** le fichier

**Exemple :**

```javascript
const password = "g07XXXXXX";  // Si votre groupe est le 7
```

>  **Sécurité** : Ne partagez jamais votre mot de passe en dehors de votre groupe !

---

## Étape 3 : Découvrir l'interface

### Ouvrir le projet

1. **Double-cliquez** sur `index.html`
2. Le projet s'ouvre dans votre navigateur par défaut
3. Vous devriez voir :
   - Une **image** d'une œuvre d'art
   - Un **chat** avec le compagnon IA
   - Des **miniatures** des scènes visitées

### Explorer l'interface

**Testez les interactions de base :**

1. Écrivez `aide` dans le chat → Vous verrez la liste des commandes
2. Écrivez `nom` → Le compagnon vous rappelle votre nom
3. Écrivez `mon nom est [VotreNom]` → Changez votre nom
4. Discutez librement avec le compagnon sur l'œuvre affichée

**Observez comment le compagnon répond :**

- Est-il pédagogique ?
- Pose-t-il des questions ?
- Guide-t-il votre réflexion ?

### Utiliser le panneau Debug

Le bouton **"Debug"** vous permet de voir exactement ce qui est envoyé à l'API et ce qu'elle répond.

**Pour l'utiliser :**

1. Cliquez sur le bouton **"Debug"** en bas de l'interface
2. Un panneau s'ouvre avec deux sections :
   - **JSON envoyé** : Ce que votre application envoie à l'API (contient le `systemPrompt`, l'historique, etc.)
   - **JSON reçu** : La réponse complète de l'API

**C'est utile pour :**

- Vérifier que votre `systemPrompt` est correctement envoyé
- Comprendre pourquoi l'IA répond d'une certaine manière
- Détecter si le marqueur `<!-- GOTO:... -->` est présent dans la réponse

**Boutons disponibles :**

- **Copier** : Copie le JSON pour le partager ou l'analyser ailleurs
- **Effacer** : Vide le panneau
- **Fermer** : Masque le panneau

> **Astuce** : Laissez le panneau Debug ouvert pendant vos tests pour voir en temps réel ce qui se passe !

---

## Étape 4 : Comprendre le rôle du compagnon IA

### Qu'est-ce que le compagnon IA ?

Le **compagnon IA** est un guide virtuel qui :

- Accompagne l'utilisateur dans l'observation des œuvres
- Pose des questions pour stimuler la réflexion
- Guide vers un **objectif pédagogique** pour chaque œuvre
- S'adapte selon les instructions que **vous** définissez

### Comment fonctionne-t-il ?

Le comportement du compagnon est défini dans le **`systemPrompt`** de chaque scène (dans `data.js`).

**Exemple** (extrait du projet) :

```javascript
systemPrompt: `
  Tu es un guide calme et attentif, spécialiste de l'histoire de l'art.
  
  Tu accompagnes l'utilisateur dans l'observation du tableau
  « Impression, soleil levant » de Claude Monet (1872).
  
  Objectif pédagogique :
  Amener l'utilisateur à comprendre que Monet ne cherche pas à 
  représenter fidèlement la réalité, mais à saisir un instant 
  et une impression visuelle.
`
```

**Le compagnon va :**

- Se présenter comme un "guide calme et attentif"
- Poser des questions sur le tableau de Monet
- Guider vers l'objectif pédagogique défini

### Testez les exemples fournis

1. Discutez avec le compagnon sur la première œuvre
2. Observez comment il guide la conversation
3. Notez :
   - Le **ton** qu'il utilise
   - Les **questions** qu'il pose
   - Comment il vous amène vers l'**objectif pédagogique**

> **Pour aller plus loin** : Consultez la section [Structure d'un bon systemPrompt](https://si3stael.github.io/tutos/tutorial#structure-dun-bon-systemprompt) du tutoriel complet.

---

## Étape 5 : Planifier votre projet

**Avant de coder**, prenez le temps de réfléchir à votre projet !

### Réfléchissez à vos scènes

**Questions à vous poser :**

1. **Quelles œuvres** allez-vous présenter ?
   - Choisissez 3 à 5 œuvres cohérentes (même artiste, même mouvement, même thème, etc.)
   
2. **Quel est l'objectif** pour chaque œuvre ?
   - Que voulez-vous que l'utilisateur comprenne ?
   - Exemple : "Comprendre l'utilisation de la perspective dans ce tableau"

3. **Comment organiser** la progression ?
   - Quelle œuvre en premier ? En dernier ?
   - Y a-t-il une histoire à raconter ?

### Définissez le rôle du compagnon

**Questions à vous poser :**

1. **Quelle personnalité** pour le compagnon ?
   - Professeur sérieux ? Guide enthousiaste ? Narrateur mystérieux ?
   
2. **Quel style d'interaction** ?
   - Pose beaucoup de questions ? Donne des explications détaillées ?
   
3. **Comment guide-t-il** l'utilisateur ?
   - Méthode socratique ? Storytelling ? Analyse technique ?

###  Exercice de planification

**Créez un document** (Word, Google Docs, etc.) avec ce tableau :

| Scène | Œuvre | Objectif pédagogique | Personnalité du compagnon | Mot-clé de transition |
|-------|-------|---------------------|---------------------------|----------------------|
| 1 | _Exemple : La Joconde_ | _Comprendre le sfumato_ | _Guide patient_ | _technique_ |
| 2 | ... | ... | ... | ... |
| 3 | ... | ... | ... | ... |

>  **Conseil** : Gardez ce document à côté de vous pendant que vous codez !

---

## Étape 6 : Modifier les scènes existantes

### Pourquoi commencer par modifier ?

Modifier les scènes existantes avant d'en créer de nouvelles vous permet de :
- Comprendre la structure du code
- Voir immédiatement l'effet de vos changements
- Vous familiariser avec le `systemPrompt`
- Éviter les erreurs de débutant

### Première modification : Changer le titre

1. Ouvrez `data.js`
2. Trouvez la première scène (ligne ~6) :
   ```javascript
   {
     id: "scene-art-02",
     title: "Impression, soleil levant",
     // ...
   }
   ```
3. Changez le titre :
   ```javascript
   title: "Mon premier test",
   ```
4. **Sauvegardez** et **rechargez** la page dans le navigateur
5. Le titre devrait avoir changé !

### Deuxième modification : Adapter le systemPrompt

1. Dans la même scène, trouvez le `systemPrompt`
2. Changez le ton du compagnon :

**Avant :**
```javascript
systemPrompt: `
  Tu es un guide calme et attentif, spécialiste de l'histoire de l'art.
  // ...
`
```

**Après :**
```javascript
systemPrompt: `
  Tu es un guide très enthousiaste et plein d'énergie, spécialiste de l'histoire de l'art.
  Tu utilises beaucoup d'émojis et d'exclamations pour rendre l'art passionnant ! 
  // ...
`
```

3. **Sauvegardez** et **rechargez** la page
4. Cliquez sur **Reset** pour redémarrer la scène
5. Observez comment le ton du compagnon a changé !

### Testez vos modifications

**Checklist de test :**
- [ ] Le titre s'affiche correctement
- [ ] Le compagnon répond avec le nouveau ton
- [ ] La conversation fonctionne toujours
- [ ] Pas d'erreur dans la console (F12)

> **Pour aller plus loin** : Consultez la section [Champs à personnaliser](https://si3stael.github.io/tutos/tutorial#champs-à-personnaliser) du tutoriel complet.

---

## Étape 7 : Utiliser la console (F12) pour déboguer

### Ouvrir la console

**Raccourcis clavier :**
- **Windows/Linux** : Appuyez sur `F12`
- **Mac** : Appuyez sur `Cmd + Option + I`

**Onglets importants :**
- **Console** : Messages de débogage et erreurs
- **Elements** : Voir le HTML de la page
- **Network** : Voir les appels à l'API

### Que voir dans la console ?

**Messages normaux** (en noir ou bleu) :
```
Application to-do list chargée
Ajout de la tâche : Acheter du pain
```
Ces messages indiquent que tout fonctionne.

**Avertissements** (en jaune) :
```
Warning: La variable 'userName' n'est pas définie
```
Pas critique mais à surveiller.

**Erreurs** (en rouge) :
```
Uncaught ReferenceError: maVariable is not defined
    at script.js:15
```
⚠️ **Attention** : Votre code a un problème !

### Utiliser console.log() dans votre code

Pour déboguer, ajoutez des `console.log()` dans vos fichiers JavaScript :

**Exemple dans `manip.js` :**
```javascript
function beforeAI(userText, scene){
    console.log("Message reçu :", userText);  // Ajoutez ceci
    console.log("Scène actuelle :", scene.id); // Et ceci
    
    let laisseAIdecider = true;
    
    if(userText.toLowerCase() === "aide"){
        console.log("Commande 'aide' détectée"); // Et ceci
        // ... reste du code
    }
    
    return laisseAIdecider;
}
```

**Dans la console, vous verrez :**
```
Message reçu : aide
Scène actuelle : scene-art-02
Commande 'aide' détectée
```

### Comprendre les erreurs

**Erreur typique :**
```
Uncaught ReferenceError: promptVars is not defined
    at data.js:25
```

**Comment la lire :**
1. **Type d'erreur** : `ReferenceError` (variable non trouvée)
2. **Message** : `promptVars is not defined` (promptVars n'existe pas)
3. **Fichier et ligne** : `data.js:25` (ligne 25 de data.js)

**Comment la corriger :**
1. Cliquez sur `data.js:25` pour aller directement à la ligne
2. Vérifiez que vous avez bien écrit `promptVars` (orthographe)
3. Vérifiez que `promptVars.js` est bien chargé dans `index.html`

> **Astuce** : Gardez **toujours** la console ouverte pendant vos tests !

---

## Prochaines étapes

Maintenant que vous avez pris en main le projet, vous pouvez :

1. **Créer vos propres scènes** → [Ajouter une nouvelle scène](https://si3stael.github.io/tutos/tutorial#ajouter-une-nouvelle-scène)
2. **Personnaliser les commandes** → [Fichier manip.js](https://si3stael.github.io/tutos/tutorial#fichier-2--manipjs--gérer-les-commandes-prédéterminées)
3. **Gérer les variables** → [Fichier promptVars.js](https://si3stael.github.io/tutos/tutorial#fichier-4--promptvarsjs--gérer-les-variables-globales-pour-les-prompts)
4. **Affiner les transitions** → [Système de transitions](https://si3stael.github.io/tutos/tutorial#système-de-transitions-entre-scènes)

**Workflow recommandé :**
1. Planifiez d'abord (Étape 5)
2. Modifiez les scènes existantes (Étape 6)
3. Créez une nouvelle scène simple
4. Testez et ajustez
5. Ajoutez progressivement plus de scènes

---

## Ressources

**Documents essentiels :**
-  [Tutoriel complet](https://si3stael.github.io/tutos/tutorial) — Guide détaillé de tous les fichiers
-  [Tutoriel Web Front-End](tutojs) — Bases de HTML, CSS, JavaScript

**En cas de problème :**
- [Section Débogage](https://si3stael.github.io/tutos/tutorial#débogage-courant) — Solutions aux problèmes courants
- [FAQ](https://si3stael.github.io/tutos/tutorial#questions-fréquentes) — Questions fréquentes

---

## Besoin d'aide ?

**Problème technique :**
1. Vérifiez la console (F12)
2. Consultez la [section Débogage](https://si3stael.github.io/tutos/tutorial#débogage-courant)
3. Demandez à votre enseignant avec un exemple précis

**Question sur le projet :**
1. Relisez ce guide
2. Consultez le [tutoriel complet](https://si3stael.github.io/tutos/tutorial)
3. Discutez avec votre groupe

---

**Bon courage et amusez-vous bien !**

N'oubliez pas : ce projet est autant une exploration artistique que technique. Prenez le temps d'expérimenter et de créer quelque chose qui vous plaît !
