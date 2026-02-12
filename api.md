<p>
<a href="https://oc-informatique.github.io/SI/starter">Démarrage</a> |
<a href="https://oc-informatique.github.io/SI/tutorial">Tutoriel complet</a> |
<a href="https://oc-informatique.github.io/SI/tutojava">Web Front-End</a> |
<a href="https://oc-informatique.github.io/SI/api">L’API ChatGPT</a>
</p>

<hr>


# API ChatGPT — Guide de fonctionnement

- [API ChatGPT — Guide de fonctionnement](#api-chatgpt--guide-de-fonctionnement)
  - [Contexte, tokens, historique et implémentation en javascript](#contexte-tokens-historique-et-implémentation-en-javascript)
  - [0. Qu'est-ce qu'une API ?](#0-quest-ce-quune-api-)
  - [1. Principe fondamental : l'API chatgpt est stateless](#1-principe-fondamental--lapi-chatgpt-est-stateless)
  - [2. Architecture d’une requête](#2-architecture-dune-requête)
    - [Structure minimale](#structure-minimale)
  - [3. Le tableau `input`](#3-le-tableau-input)
  - [4. Les roles](#4-les-roles)
    - [system](#system)
    - [user](#user)
    - [assistant](#assistant)
    - [Le contexte : règle absolue](#le-contexte--règle-absolue)
  - [5. Exemple d’historique valide](#5-exemple-dhistorique-valide)
  - [6. Exemple de JSON envoyé à chatgpt](#6-exemple-de-json-envoyé-à-chatgpt)
  - [7. Exemple de JSON reçu en retour de chatgpt](#7-exemple-de-json-reçu-en-retour-de-chatgpt)
  - [8. Implémentation en javascript](#8-implémentation-en-javascript)
    - [Appel à l'API chatgpt dans le code](#appel-à-lapi-chatgpt-dans-le-code)
  - [9. Tokens](#9-tokens)
  - [10. Erreurs courantes](#10-erreurs-courantes)
  - [11. Résumé](#11-résumé)

## Contexte, tokens, historique et implémentation en javascript

Dans ce projet, vous allez interagir avec ChatGPT à travers son API, c'est-à-dire que vous allez envoyer vos requêtes à travers un programme et non en passant par le site web dont vous avez l'habitude.
Ce document décrit le fonctionnement d’une requête à l’API ChatGPT : gestion du **contexte**, notion de **tokens**, inclusion de **l’historique de conversation** et **exemple d’implémentation en javascript**.

---

## 0. Qu'est-ce qu'une API ?

Une API (Application Programming Interface) est une interface qui permet à des programmes de communiquer entre eux. Dans le cas de l’API ChatGPT, elle permet à votre programme d’envoyer des requêtes à ChatGPT et de recevoir des réponses, sans passer par une interface utilisateur graphique. L’API est un point d’entrée pour interagir avec le modèle de langage de manière programmatique.

**Une API définit :**

- ce que tu peux demander (ex : “la météo étant donné une position gps”)
- comment le demander (format, URL, paramètres)
- ce que tu reçois en retour (souvent du JSON)
- les règles d’utilisation (limites, coûts, etc.)

**Exemples d’API :**

- API de géolocalisation : obtenir la position d’un utilisateur à partir de son adresse IP
- API de traduction : traduire du texte d’une langue à une autre
- API de paiement : traiter des transactions financières en ligne
- API de ChatGPT : envoyer des requêtes textuelles et recevoir des réponses générées par le modèle de langage
- API de reconnaissance d’image : analyser une image et en extraire des informations (ex : Google Vision API)
- API de données météorologiques : obtenir les prévisions météo pour une localisation donnée (ex : OpenWeatherMap API)

---

## 1. Principe fondamental : l'API chatgpt est stateless

L’API ChatGPT est **stateless**.

Cela signifie :

- aucune mémoire persistante
- aucun état conservé entre deux requêtes
- chaque appel est évalué indépendamment

👉 Toute information non envoyée dans la requête **n’existe pas** pour le modèle.

---

## 2. Architecture d’une requête

Une requête vers l’API contient :

- un modèle (`model`)
- un tableau ordonné d'entrées (le tableau `input`)
- des paramètres de génération (`temperature`, `max_tokens`), ces paramètres influencent la réponse du modèle, mais ne sont pas obligatoires, s'ils ne sont pas fournis, des valeurs par défaut sont utilisées.

Le tableau `input` est le cœur de la requête. C’est lui qui contient le contexte : l'entrée qui donne des instructions de départ au modèle ("role":"system"), les demandes de l’utilisateur ("role":"user") et les réponses précédentes du modèle ("role":"assistant"). Le contexte est **exclusivement** ce qui est présent dans le tableau `input`.

### Structure minimale

La requête est un fichier json dont voici un exemple minimal :

```json
{
  "model": "gpt-4.1",
  "input": [
    { "role": "system", "content": "Tu es un assistant pédagogique clair et précis." },
    { "role": "user", "content": "Explique le concept de token." }
  ]
}
```

Le champ `model` spécifie le modèle à utiliser (ici gpt-4.1).
Le modèle va répondre en fonction des instructions données dans l’entrée `system` et de la demande de l’utilisateur dans l’entrée `user`.

---

## 3. Le tableau `input`

Le tableau `input` contient les entrées envoyées par l’utilisateur et les réponses précédentes du modèle renvoyées par le développeur. C'est la source unique du contexte.

Le modèle ne voit que le tableau `input`.
Dans l’API ChatGPT, le champ `input` correspond au tableau entrées.

Chaque entrée du tableau contient :

- role : type de l'entrée (system, user, assistant)

- content : contenu textuel

⚠️ L’ordre des entrées est critique.
💡 Si ce n’est pas dans `input`, ça n’existe pas.
ChatGPT n’a pas de mémoire.
C’est ton JSON qui se souvient.

---

## 4. Les roles

### system

Définit le comportement global du modèle, les instructions de départ (règles, ton et contraintes).

```json
{ "role": "system", "content": "Tu es un assistant pédagogique clair et précis." }
```

### user

Demandes envoyées par l'utilisateur.

```json
{ "role": "user", "content": "Explique le concept de token." }
```

### assistant

Réponses précédentes du modèle, à renvoyer pour maintenir le contexte.

```json
{ "role": "assistant", "content": "Un token est une unité de texte..." }
```

### Le contexte : règle absolue

- ❌ Le modèle ne se souvient de rien.
- ❌ Il n’existe aucune mémoire implicite.
- ✅ Le contexte = l’intégralité du tableau `input` envoyé.

---

## 5. Exemple d’historique valide

Dans le tableau `input`, il faudra envoyer l'historique de la conversation si vous voulez que chatgpt en tienne compte.
Rappel : l'ordre dans le tableau `input` **compte**.
Exemple de tableau `input` avec historique.

```json
[
  { "role": "system", "content": "Tu es un assistant technique." },
  { "role": "user", "content": "Qu’est-ce qu’un token ?" },
  { "role": "assistant", "content": "Un token est une unité..." },
  { "role": "user", "content": "Pourquoi est-ce important ?" }
]
```

Dans ce tableau chatgpt comprend :

- les instructions initiales qui définissent son comportement et son ton
- les demandes précédentes de l'utilisateur
- ce qui a déjà été expliqué (les réponses de l’assistant)
- la demande actuelle

---

## 6. Exemple de JSON envoyé à chatgpt

Un fichier JSON est un document texte structuré. C'est un format d'échange de données très utilisé dans les API web. Il est aussi très utilisé dans les bases de données NoSQL comme MongoDB, les échanges de données entre serveurs web et clients, et pour la configuration d'applications. Ci-dessous un exemple de JSON envoyé à l'API ChatGPT.

``` json
{
  "model": "gpt-4.1-mini",
  "temperature": 0.3,
  "input": [
    {
      "role": "system",
      "content": "Tu es un guide calme et attentif, spécialiste de l’histoire de l’art.\n\n        Tu accompagnes l’utilisateur dans l’observation du tableau\n        « Impression, soleil levant » de Claude Monet (1872).\n\n        Règles de comportement :\n        - Tu ne donnes pas de réponse scolaire ou encyclopédique.\n        - Tu encourages l’utilisateur à décrire ce qu’il ressent, ce qu’il perçoit visuellement.\n        - Tu poses des questions ouvertes, simples, accessibles.\n        - Tu valorises les sensations : lumière, couleur, mouvement, impression.\n        - Tu évites les mots techniques tant que l’utilisateur ne les introduit pas lui-même.\n\n        Objectif pédagogique :\n        Amener l’utilisateur à comprendre que Monet ne cherche pas à représenter fidèlement la réalité, \n        mais à saisir un instant et une impression visuelle.\n\n        Gestion de la progression (obligatoire) :\n      - Après **le deuxième message de l’utilisateur**, tu dois conclure,\n        même si l’objectif pédagogique n’est pas formulé explicitement par l’utilisateur.\n      - Si l’utilisateur comprend plus vite, tu conclus immédiatement.\n      - La conclusion doit être claire, brève (4–6 phrases maximum),\n        et expliciter l’objectif pédagogique.\n\n      Déclenchement de la scène suivante :\n      - Lorsque l’utilisateur tape le mot-clé exact « structure »\n        **ou** lorsque tu conclus pédagogiquement,\n        tu termines ton message en incluant exactement :\n        <!-- GOTO:scene-art-03 -->\n      - Tu indiques explicitement que l’œuvre suivante a été débloquée."
    },
    {
      "role": "user",
      "content": "Décris la scène et commence la visite…"
    },
    {
      "role": "assistant",
      "content": "Regardons ensemble ce tableau, « Impression, soleil levant » de Monet. Que vois-tu d’abord ? Quelle est la première chose qui attire ton regard dans cette scène ? Peut-être la lumière, les couleurs, ou quelque chose d’autre ? N’hésite pas à me dire ce que tu ressens en regardant cette image."
    },
    {
      "role": "user",
      "content": "c'est un soleil chaud sur un port"
    },
    {
      "role": "assistant",
      "content": "Oui, ce soleil semble vraiment chaud, presque brûlant, même s’il est à peine levé. Et ce port, comment le perçois-tu ? Est-il calme, animé, ou peut-être un peu flou ? Qu’est-ce qui te fait ressentir cela ? Quels détails ou quelles couleurs te parlent le plus dans cette partie du tableau ?"
    },
    {
      "role": "user",
      "content": "les reflets rouges sur la mer"
    }
  ]
}
```

---

## 7. Exemple de JSON reçu en retour de chatgpt

```json
{
  "id": "resp_0324f442537fe3e000697bf23c40f881928cec9ed1cc2139ed",
  "object": "response",
  "created_at": 1769730620,
  "status": "completed",
  "background": false,
  "billing": {
    "payer": "openai"
  },
  "model": "gpt-4.1-mini-2025-04-14",
  "output": [
    {
      "id": "msg_0324f442537fe3e000697bf23d342481928225d74dcae7df25",
      "type": "message",
      "status": "completed",
      "content": [
        {
          "type": "output_text",
          "annotations": [],
          "logprobs": [],
          "text": "Tu as remarqué ces reflets rouges sur l’eau, c’est très juste. Ils semblent danser avec la lumière du soleil, n’est-ce pas ? Comment trouves-tu le mouvement de l’eau ? Est-ce qu’elle paraît tranquille, agitée, ou plutôt mystérieuse ? Et cette lumière rouge, est-ce qu’elle te donne une impression de chaleur, de douceur, ou autre chose ? \n\nCe tableau ne cherche pas à montrer chaque détail avec précision, mais plutôt à capturer ce que Monet a ressenti à cet instant précis, cette impression fugace de lumière et de couleur. C’est comme si le peintre voulait nous faire vivre ce moment, plus que le décrire exactement. \n\nSi tu veux, on peut continuer à explorer ensemble, ou passer à une autre œuvre. Que préfères-tu ?  \n<!-- GOTO:scene-art-03 -->  \nL’œuvre suivante a été débloquée."
        }
      ],
      "role": "assistant"
    }
  ],
  "temperature": 0.3,
  "usage": {
    "input_tokens": 518,
    "output_tokens": 185,
    "total_tokens": 703
  },
}
```

---

## 8. Implémentation en javascript

⚠️ Sécurité
Ne pas publier l'ensemble de votre code sur internet. La clé de connexion avec l'API n'est pas sécurisée de manière satisfaisante. Si vous la publiez, des tiers pourraient l'utiliser à votre place et nous facturer des coûts importants.

Si vous êtes intéressé l'implémentation de la conversation avec chatgpt se trouve dans le fichier app.js (**nous vous conseillons de ne pas modifier ce fichier**).

### Appel à l'API chatgpt dans le code

Dans l'exemple de code javascript suivant, on crée un tableau conversation (qui sera notre `input`) et on commence par spécifier le rôle que va prendre notre API.
On ajoute ensuite la demande de l'utilisateur.
La fonction callChatGPT() communique avec l'API.
On stoque la réponse de l'API dans la variable reply.

``` javascript
const conversation = [
  {
    role: "system",
    content: "Tu es un assistant pédagogique clair et structuré."
  }
];
addUserMessage("Explique ce qu’est un token.");
const reply = await callChatGPT();
console.log(reply);
```

## 9. Tokens  

Un token est une unité de texte utilisée par le modèle pour lire et produire du contenu. Un token n’est pas forcément un mot : il peut correspondre à un mot entier, une partie de mot, un signe de ponctuation ou un espace. Lorsqu’une requête est envoyée à l’API, tout le contenu du tableau input est découpé en tokens, tout comme la réponse générée. Le nombre total de tokens (tokens d’entrée + tokens de sortie) est important, car il détermine les limites du modèle, le coût de la requête et la longueur maximale de la réponse (max_tokens). Plus l’historique inclus dans `input` est long, plus le nombre de tokens consommés augmente.

## 10. Erreurs courantes

-  ❌ Oublier de renvoyer les entrées assistant
-  ❌ Changer l’ordre des entrées
-  ❌ Croire que ChatGPT “se souvient”
-  ❌ Envoyer seulement la dernière question

## 11. Résumé

Le modèle ne raisonne qu’avec le contexte explicitement fourni.
Toute information absente n’existe pas.

- API ChatGPT = stateless

- contexte = tableau `input`

- historique = responsabilité du développeur

ChatGPT ne lit pas une conversation.
Il lit un tableau d'entrées à chaque appel.
  
👉 Pour chaque appel API, pose-toi toujours la question :
« Ai-je envoyé tout ce que le modèle doit savoir pour répondre correctement ? »
