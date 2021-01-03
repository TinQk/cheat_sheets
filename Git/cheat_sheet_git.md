# Cheat_Sheet (merde merde ?)
Quelques trucs à se rappeler

Mise en forme des README : _[markdown](https://guides.github.com/features/mastering-markdown/)_

## Git/GitHub
    Sommaire :
    - Quelques définitions
    - Créer un repo en local puis le sauvegarder sur GitHub
    - Quand un repo local est modifié
    - Git/GitHub en groupe

------------------------------------------------
### Quelques définitions :

    - Git : logiciel de versionning et de gestion d’un programme - local
    - GitHub : hébergement de programmes – distribution to community - en ligne

    - commit : version de code
    - fork : copie à un instant t d’un programme – développement parallèle sans lien avec l’initial
    - branch : new development in a program – avec lien avec l’initial
    - remote repository : dépôt distant => "Un dépôt distant (en anglais remote repository) est un dépôt GIT, 
    tout à fait similaire à un dépôt local, mais acessible à distance via une URL."

    - git init : initialisation d'un repository dans le repertoire commun - uniquement si création à partir 
    de l'ordi. Si créé sur GitHub puis cloner pas la peine.
    - git add fichier : ajout du fichier au repository
    - git log : état du repos - historique de tous les commits
    - git status : permet de voir quels fichiers ont été modifiés
    - git commit -m [nom_commit] : créer un commit
    - git push origin master : mettre en ligne (sur GitHub) le projet
    - git checkout [numéro_commit] : se positionner à la version ciblée par le numéro (SHA)
    - git checkout master : revenir à la version master
    - git branch : visualisation des différentes branch du repos
    - git clone https://github.com/ton_username/le_nom_de_ton_repo : cloner repos depuis github


***************************************************************************
### Créer un repo en local puis le sauvegarder sur GitHub
1. mkdir [nom_dossier] _# créer un dossier local_
2. cd [nom_dossier] _# se positionner dedans_
3. git init _# initialiser le dossier (notamment création du dossier .git)_
4. git commit -m "initialisation" _# premier commit_
5. Sur GitHub créer un repos avec le même nom
6. git remote add origin https://github.com/[pseudo_github]/nom.git _# En étant dans le dossier [nom_dossier]_


***************************************************************************
### Quand un repo local est modifié
1. git add . _# ajoute les fichiers modifiés au repository_
2. git commit -m "nom du commit"
3. git push origin master _# mettre à jour le master sur GitHub_

***************************************************************************

### **Git/GitHub en groupe**

*Le repos est de la forme :*
  - une branche master
  - une branche [nom_de_la_branche]

#### Je travaille sur la branche 'nom_de_la_branche'

--> pour vérifier : git branch

1. git add [nom_fichier] _# ajout des fichiers à intégrer dans le commit (. si on veut tout le répertoire courant)_
2. git checkout [nom_fichier] _# si je veux exclure des fichiers du commit_
3. git commit -m "message"
4. git checkout master
5. git pull origin master _# mettre à jour son dépot local_
6. git merge master _# changement de la branche de travail_
7. git checkout master
8. git merge [nom_de_la_branche]
9. git push origin master

#### Oups, je travaille sur la branche master

--> pour vérifier : git branch

1. git add [nom_fichier] _# ajout des fichiers à intégrer dans le commit (. si on veut tout le répertoire courant)_
2. git checkout [nom_fichier] _# si je veux exclure des fichiers du commit_
3. git commit -m "message"
4. git checkout [nom_de_la_branche]
5. git merge master
6. git checkout master
7. git pull origin master _# mettre à jour son dépot local_
8. git checkout [nom_de_la_branche] _# changement de la branche de travail_
9. git merge master
10. git checkout master
11. git merge [nom_de_la_branche]
12. git push origin master
