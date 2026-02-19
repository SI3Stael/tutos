# À savoir pour le QCM

## API ChatGPT (<a href="https://si3stael.github.io/tutos/api">L’API ChatGPT</a>)

- Savoir ce qu'est une API.
- L'API ChatGPT est **stateless** : aucune mémoire entre deux requêtes.
- Les champs **obligatoires** d'une requête : `model` et `input` seulement. Savoir à quoi ces champs correspondent.
- Les champs **optionnels** : `temperature`, `max_tokens`.
- Le rôle **system** : définit le comportement global de l'IA.
- Le rôle **user** : messages de l'utilisateur.
- Le rôle **assistant** : réponses précédentes de l'IA, à renvoyer pour maintenir le contexte.
- L'**ordre** des entrées dans `input` est critique (system en premier, puis ordre chronologique).
- Un **token** : unité de texte (mot, partie de mot, ponctuation, espace) — tokens d'entrée ET de sortie sont comptabilisés.
- Si l'historique n'est pas inclus dans `input`, le modèle n'en a aucun souvenir.

## Projet Galerie — Fichiers (<a href="https://si3stael.github.io/tutos/starter">Démarrage</a>)

- Nous pouvons poser toutes questions dans le guide de démarrage.
- `data.js` : définit les scènes (œuvres, images, prompts).
- `manip.js` : gère les commandes prédéterminées via `beforeAI()`.
- `promptVars.js` : variables globales injectables dans les prompts avec `{% raw %}{{nomVariable}}{% endraw %}`.
- `app.js` : ne pas modifier — gère les appels API.

## manip.js  (<a href="https://si3stael.github.io/tutos/tutorial">Tutoriel complet</a>)

- `beforeAI()` intercepte le message avant l'appel à l'IA.
- Si `beforeAI()` retourne `false` → l'IA n'est pas appelée.
- Pour ajouter une commande (ex: "couleur bleue") → `else if` dans `beforeAI()` dans `manip.js`.
- Commandes existantes : `aide`, `nom`, `mon nom est X`.

## promptVars.js (<a href="https://si3stael.github.io/tutos/tutorial">Tutoriel complet</a>)

- Contient les variables globales réutilisables dans tous les prompts.
- Syntaxe dans le prompt : `{% raw %}{{userName}}{% endraw %}`, `{% raw %}{{age}}{% endraw %}`, etc.
- On peut modifier les variables dynamiquement dans `manip.js`.

## data.js (<a href="https://si3stael.github.io/tutos/tutorial">Tutoriel complet</a>)

- `systemPrompt` : instructions cachées qui définissent le comportement de l'IA pour la scène (`tutorial.md`).
- `firstUserMessage` : premier message envoyé à l'IA comme message utilisateur (`tutorial.md`).
- Transition entre scènes : l'IA inclut `<!-- GOTO:scene-id -->` dans sa réponse (`tutorial.md`).
- Savoir comment on change les images d'une scène : en modifiant le champ `image` dans `data.js` (`tutorial.md`).
- En général il faut comprendre la différence entre transition par IA et transition via logique conditionnelle.

## Normes APA (<a href="https://si3stael.github.io/tutos/apa">Normes APA</a>)

- Les normes APA : ensemble de règles pour citer des sources dans les travaux académiques.
- Citations dans le texte : format `(Auteur, année)`.
- Différence entre référence et citation.
- Bibliographie en fin de document, classée alphabétiquement.
- Pas de notes de bas de page avec les sources en APA.
- Dans Google Docs : Outils → Citations → style APA.

## Analyse de sources (<a href="https://si3stael.github.io/tutos/apa">Normes APA</a>)

- Connaître les 7 critères qui permettent d'évaluer la qualité d'une source.
- Savoir comment une IA serait évaluée selon ces critères.
- Savoir que les IA actuelles ne sont pas fiables pour fournir des sources de qualité (manque de transparence, biais, etc.).
- Savoir que les IA ne peuvent pas être utilisées comme sources dans un travail académique selon les normes APA.
- Savoir que les IA peuvent être utilisées pour aider à trouver des sources, mais que ces sources doivent être vérifiées et citées correctement.
