# Biblio

Biblio est un petit programme en ligne de commande qui gère les prêts de livres d'une bibliothèque associative. Il est destiné aux bénévoles de l'association : il ne demande aucune connaissance en programmation, seulement de taper quelques commandes.

## Prérequis

- Python 3 (aucune bibliothèque externe à installer).
- GitHub Desktop, pour récupérer le projet.

Pour vérifier que Python est installé :

```
python --version
```

Résultat attendu (le numéro dépend de votre installation) :

```
Python 3.x.x
```

Sous macOS ou Linux : `python3 --version`. Sous Windows, si `python` ne marche pas : `py --version`.

## Installation

1. Cloner le dépôt avec GitHub Desktop :
   File > Clone repository > onglet URL.
2. Repository > Open in Command Prompt.
3. Créer la base de démonstration (à faire une fois, avant le reste) :

```
python biblio.py init
```

Résultat attendu :

```
Base initialisee : 6 livres, 3 membres.
```

Sous macOS ou Linux : `python3`. Sous Windows, si `python` ne marche pas : `py`.

Attention : `init` remet les données de départ. Relancer cette commande efface les prêts enregistrés depuis.

## Utilisation

Toutes les commandes se tapent dans le dossier du projet, après avoir lancé `init` (voir Installation). Dans les exemples, remplacez `python` par `python3` (macOS, Linux) ou `py` (Windows) si besoin. Les résultats ci-dessous se suivent : chaque commande part de l'état laissé par la précédente.

### Lister les livres

```
python biblio.py livres
```

Résultat attendu :

```
[1] L'Etranger (Albert Camus) : disponible
[2] Dune (Frank Herbert) : emprunte
[3] Le Petit Prince (Antoine de Saint-Exupery) : disponible
[4] Fondation (Isaac Asimov) : disponible
[5] Les Miserables (Victor Hugo) : disponible
[6] Neuromancien (William Gibson) : disponible
```

### Chercher un livre

```
python biblio.py chercher Dune
```

Résultat attendu :

```
[2] Dune (Frank Herbert)
```

Si rien ne correspond, le programme affiche `Aucun livre trouve.`

### Emprunter un livre

La commande prend le numéro du livre, puis le numéro du membre (1 : Alice Martin, 2 : Bilal Haddad, 3 : Chloe Nguyen).

```
python biblio.py emprunter 1 1
```

Résultat attendu :

```
Emprunt enregistre : livre 1, membre 1.
```

Le programme refuse l'emprunt dans deux cas :

```
python biblio.py emprunter 2 3
```

```
Erreur : livre 2 deja emprunte.
```

```
python biblio.py emprunter 3 999
```

```
Erreur : membre 999 introuvable.
```

### Rendre un livre

```
python biblio.py rendre 1
```

Résultat attendu :

```
Retour enregistre pour le livre 1.
```

### Voir les retards

Cette commande liste les livres non rendus depuis plus de 14 jours.

```
python biblio.py retards
```

Résultat attendu (le nombre de jours dépend de la date du jour) :

```
Dune, emprunte par Alice Martin : 255 jours de retard
```

S'il n'y a aucun retard, le programme affiche `Aucun retard.`

## Tests

Depuis le dossier du projet :

```
python -m unittest
```

Résultat attendu :

```
...
----------------------------------------------------------------------
Ran 0 tests in 0.000s

OK
```

La ligne `OK` à la fin signifie que tous les tests passent. Sous macOS ou Linux : `python3 -m unittest`. Sous Windows, si `python` ne marche pas : `py -m unittest`.

## Structure du projet

```
biblio.py          le programme (toutes les commandes)
README.md          ce fichier
docs/
  circulation.md   comment l'information circule dans l'équipe
  adr/             les décisions techniques (ADR)
exercices/         les exercices des séances
.github/           les modèles d'issues et de pull requests
biblio.db          la base de données, créée par la commande init
```

## Contribuer

1. **Issue** : toute modification commence par une issue, avec le bon modèle (bug, évolution ou question). Un seul problème par issue, un titre qui dit ce qui se passe et où.
2. **Branche** : on ne travaille jamais directement sur `main`. Créer une branche à partir de `main`, nommée `type/n°-mots-cles`, par exemple `fix/3-double-pret` ou `docs/5-readme`.
3. **Commit** : un message clair qui commence par le type de changement, par exemple `fix: refuse l'emprunt d'un livre deja emprunte` ou `docs: section utilisation du README`.
4. **Pull request** : décrire le contexte avec `Closes #n` (le numéro de l'issue), les changements, l'impact et comment tester. Choisir un camarade comme relecteur.
5. **Review** : le relecteur teste, commente et donne un verdict (Approve ou Request changes). Seule une PR approuvée est mergée, puis la branche est supprimée.

## Auteurs

- Ahmed Salah
- Paul Benoit