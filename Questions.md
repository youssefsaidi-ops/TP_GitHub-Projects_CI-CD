# Question 1

git init crée un dépôt Git, git add sélectionne les fichiers modifiés pour les préparer à la validation, et git commit enregistre définitivement ces changements dans l’historique du projet avec un message descriptif.

# Question 2

1. Un dépôt local est une copie du projet stockée sur ton ordinateur, tandis qu’un dépôt distant est une version hébergée en ligne sur un serveur comme GitHub, permettant de partager et de synchroniser le code avec d’autres personnes.
2. "origin" est le nom par défaut donné au dépôt distant principal, ce qui permet de l’appeler facilement dans les commandes Git.
3. La commande ( git push ) envoie les commits locaux vers le dépôt distant pour les partager et les mettre à jour.
4. L’option "-u" dans ( git push -u origin main ) permet de lier la branche locale `main` à la branche distante `origin/main`, afin que les futurs `git push` et `git pull` soient plus simples à exécuter.

# Question 3

Un environnement virtuel permet d’isoler les dépendances du projet pour éviter les conflits entre versions de bibliothèques et garantir un fonctionnement stable, tandis qu’un test de division par zéro peut sembler réussir s’il n’est pas déclenché dans les bonnes conditions ou s’il n’est pas vérifié correctement, même si le programme réel lève bien une exception au moment de l’exécution.

# Question 4

Le premier push sur `main` déclenche automatiquement la CI parce que le workflow est configuré avec l’événement `push` sur la branche `main`, donc un simple envoi de code vers cette branche suffit à lancer les tests, sans avoir besoin d’une pull request.

# Question 5

Le test détecte la régression parce que la fonction `add` a été modifiée et que `pytest` compare le résultat attendu à celui réellement obtenu, ce qui fait échouer l’assertion ; le journal montre en détail le nom du test, la valeur attendue, la valeur obtenue et la pile d’exécution, alors que l’icône rouge ne donne que le signal global de l’échec.


# Compte rendu TP : GitHub et intégration continue (CI/CD)

## 1. Présentation du projet
Ce TP avait pour objectif de prendre en main Git, GitHub et la mise en place d'un workflow d'intégration continue avec GitHub Actions. Le support utilisé est un petit projet Python de calculatrice avec des tests unitaires.

* **Dépôt GitHub :** `TP_GitHub-Projects_CI-CD`
* **Lien du dépôt :** https://github.com/youssefsaidi-ops/TP_GitHub-Projects_CI-CD
* **Branche principale :** `main`

## 2. Organisation du dépôt
L'arborescence du projet est découpée de façon logique pour séparer le code des tests et de la configuration :

* `app/` : le code source Python de la calculatrice.
* `tests/` : les fichiers de tests unitaires exécutés avec `pytest`.
* `.github/workflows/` : le fichier YAML qui configure la CI GitHub Actions.
* `requirements.txt` et `README.md` : les dépendances du projet et la documentation.

## 3. Fonctionnement de Git, GitHub et des Pull Requests
Pour ce TP, **Git** m'a permis de gérer les versions en local et d'envoyer mes modifications vers **GitHub** (via `add`, `commit` et `push`).

Plutôt que de coder directement sur `main`, j'ai créé une branche de travail (`fix/add`) et ouvert une **Pull Request** (`#1`). L'intérêt de la Pull Request est de pouvoir comparer ma branche avec `main` et de lancer automatiquement les vérifications avant de fusionner (*merge*) le code.

* **Lien de la Pull Request :** https://github.com/youssefsaidi-ops/TP_GitHub-Projects_CI-CD/pull/1

## 4. Détection et correction du bug
Lors du premier envoi sur la Pull Request, le workflow est passé au **rouge** à cause du test `test_add`. En regardant le code dans `app/calculator.py`, la fonction `add` avait été modifiée pour faire une soustraction (`return a - b`) au lieu d'une addition.

J'ai corrigé l'erreur en remettant la bonne opération :
```python
return a + b
```

Après avoir poussé ce correctif sur la même branche, GitHub Actions a relancé les tests et la Pull Request est passée au **vert**, ce qui m'a permis de la fusionner proprement dans `main`.

## 5. Test en local vs CI sur GitHub
* **En local :** On lance `pytest` directement sur notre PC (dans un environnement virtuel `.venv`) pour vérifier rapidement notre code pendant qu'on développe. L'inconvénient, c'est que ça dépend de la configuration de notre propre machine.
* **La CI (GitHub Actions) :** À chaque `push` ou `pull request`, GitHub lance automatiquement les tests sur un serveur virtuel vierge. Ça permet d'être sûr que le code fonctionne partout de la même manière et d'éviter d'intégrer des bugs sur la branche principale.

## 6. Captures d'écran

### Arborescence du dépôt sur la branche `main`
![Arborescence du projet](Capture%20d%27%C3%A9cran%202026-11-12%20113242.png)

### Pull Request : contrôle rouge (échec du test)
![Contrôle rouge](Capture%20d%27%C3%A9cran%202026-11-12%20112803.png)

### Pull Request : contrôle vert (tests validés après correction)
![Contrôle vert](Capture%20d%27%C3%A9cran%202026-11-12%20113032.png)


