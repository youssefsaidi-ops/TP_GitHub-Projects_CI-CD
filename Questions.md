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

## 8. Bilan et compte rendu

Le dépôt GitHub utilisé est `TP_GitHub-Projects_CI-CD` et son URL est `https://github.com/youssefsaidi-ops/TP_GitHub-Projects_CI-CD`, la branche principale utilisée est `main`, l’arborescence du projet est visible dans le dépôt GitHub, la pull request permet de comparer une branche de travail avec `main` pour vérifier le contrôle rouge puis le contrôle vert, le test en échec est `test_add` car la fonction `add` a été remplacée par une soustraction, et la correction a consisté à rétablir `return a + b` ; un test exécuté localement sert à vérifier le code sur son ordinateur, tandis qu’une CI exécutée par GitHub automatise et standardise cette vérification pour tout le monde sur une machine propre et reproductible.

**Conclusion :** Git conserve l’historique des changements ; GitHub héberge le dépôt et facilite le travail par pull request ; pytest exécute les tests ; GitHub Actions automatise leur exécution.
