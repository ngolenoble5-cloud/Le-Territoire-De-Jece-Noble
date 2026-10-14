# Le Territoire De Jece Noble — V3 (construction)

Jeu de quiz francophone en arène multijoueur, interface rouge/noir, serveur Node.js + Socket.IO et classements globaux.

## Règles implémentées dans cette version
- 50 catégories officielles ; une catégorie est tirée au hasard à chaque manche.
- Départ automatique dès que 2 joueurs sont présents dans une salle.
- 20 questions par manche, 20 secondes par question, quatre réponses A/B/C/D.
- Points de base = seconde écoulée (ex. réponse correcte à la 18e seconde = 18 points). Bonus par réponse correcte : +5 entre la 15e et avant la 17e seconde ; +10 de la 17e à la 20e seconde. Mauvaise réponse ou absence de réponse = 0.
- Bonus de manche : +20 si au moins 10 bonnes réponses ont été données en moins de 15 s chacune ; sinon +30 si au moins 10 ont été données en moins de 17 s chacune ; +50 pour 20/20. Les deux bonus de série rapide ne se cumulent pas entre eux ; le bonus parfait s'ajoute.
- Vainqueur de manche : meilleur score ; en cas d'égalité, temps cumulé le plus faible sur les bonnes réponses.
- Proclamation du vainqueur, pause de 6,5 s, puis nouvelle manche automatique.
- Classements général et quotidien ; persistance des scores via PostgreSQL.
- Voix de l'animateur activable/désactivable dans le navigateur.

## Dépendances indispensables
Node.js 18+ et une base PostgreSQL pour sauvegarder durablement les scores. Configure côté serveur `OPENAI_API_KEY` pour la génération des questions dans les 50 catégories et `DATABASE_URL` pour les classements persistants. Sans clé IA, le serveur refuse de démarrer une manche complète : la banque de secours n'est pas encore assez grande pour 20 questions uniques dans chaque catégorie.

## Démarrage local
```bash
npm install
npm start
```
Puis ouvre `http://localhost:3000`. Vérifie la configuration sur `http://localhost:3000/health`.

## Déploiement Render
Le fichier `render.yaml` contient le service Node. Ajoute les variables secrètes `OPENAI_API_KEY` et `DATABASE_URL` dans le tableau de bord Render. GitHub Pages seul ne peut pas exécuter le serveur Node/Socket.IO.

## Fichiers
- `index.html` : interface du jeu
- `multiplayer-client.js` : interface de l'arène en direct
- `server.js` : règles, chronomètre, calcul des scores, questions IA, classements
- `render.yaml` : configuration d'hébergement
- `INSTALLATION.txt` : étapes de configuration

## Statut honnête
Cette archive contient les modifications V3 préparées et les vérifications syntaxiques JavaScript. Elle n'a pas été déployée sur Render ni reliée automatiquement à GitHub ; la connexion PostgreSQL, la clé IA, les tests multijoueurs en ligne et la publication restent à effectuer.
