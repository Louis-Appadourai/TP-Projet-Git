# tp-bachelor

## 0 Initialiser le dépôt

Initialise un dépôt Git local dans le dossier courant :

```bash
git init
```

Résultat : Initialized empty Git repository in /Users/appadourailouis/Documents/3W Academy Bachelor 1/UE4/Projet-Git/.git/

## 1 copie le projet depuis le dépôt initial

```bash
git clone https://github.com/cecilev-axe/tp-bachelor.git
```

Résultats du git clone :  
remote: Enumerating objects: 10, done.  
remote: Counting objects: 100% (10/10), done.  
remote: Compressing objects: 100% (6/6), done.  
remote: Total 10 (delta 0), reused 10 (delta 0), pack-reused 0 (from 0)  
Receiving objects: 100% (10/10), done.

## Vérifie l’état du dépôt (aucun changement pour l’instant)

```bash
git status
```

Résultats du git status :  
On branch main  
Your branch is up to date with 'origin/main'.  
nothing to commit, working tree clean

## 2 Changer l’origine (remote)

## Supprime le lien vers le dépôt initial

```bash
git remote remove origin
```

## Relie le dépôt local à ton dépôt GitHub personnel

```bash
git remote add origin https://github.com/Louis-Appadourai/TP-Projet-Git.git
```

## 3 Vérifie que le nouveau remote est bien configuré

```bash
git remote -v
```

Résultats du git remote -v :  
origin https://github.com/Louis-Appadourai/TP-Projet-Git.git (fetch)  
origin https://github.com/Louis-Appadourai/TP-Projet-Git.git (push)

## nvoie tout le contenu du dépôt local vers ton dépôt GitHub.

```bash
git push -u origin main
```

Résultats du push réussie :  
Enumerating objects: 10, done.  
Counting objects: 100% (10/10), done.  
Delta compression using up to 16 threads  
Compressing objects: 100% (6/6), done.  
Writing objects: 100% (10/10), 2.03 KiB | 2.03 MiB/s, done.  
Total 10 (delta 0), reused 10 (delta 0), pack-reused 0 (from 0)  
To https://github.com/Louis-Appadourai/TP-Projet-Git.git  
* [new branch]        main -> main  
branch 'main' set up to track 'origin/main'.

## Vérifie l’état du dépôt (montre que index.html a été modifié)

```bash
git status
```

Résultats :  
On branch main  
Your branch is up to date with 'origin/main'.

Changes not staged for commit:  
(use "git add <file>..." to update what will be committed)  
(use "git restore <file>..." to discard changes in working directory)  
modified: index.html  

no changes added to commit (use "git add" and/or "git commit -a")

## 4 Ajouter une nouvelle fonctionnalité (4ᵉ image et dot)

## Prépare le fichier pour le commit

```bash
git add index.html
```

## Enregistre la modification localement avec un message clair

```bash
git commit -m "Ajout d'une quatrième image et d'un dot supplémentaire"
```

Résultats du git commit :  
[main d6c1d66] Ajout d'une quatrième image et d'un dot supplémentaire  
1 file changed, 11 insertions(+), 3 deletions(-)

## 5 Envoie le commit sur GitHub

```bash
git push
```

Résultats du git push :  
Enumerating objects: 5, done.  
Counting objects: 100% (5/5), done.  
Delta compression using up to 16 threads  
Compressing objects: 100% (3/3), done.  
Writing objects: 100% (3/3), 476 bytes | 476.00 KiB/s, done.  
Total 3 (delta 1), reused 0 (delta 0), pack-reused 0 (from 0)  
remote: Resolving deltas: 100% (1/1), completed with 1 local object.  
To https://github.com/Louis-Appadourai/TP-Projet-Git.git  
d94cb86..d6c1d66   main -> main

## vérifie que le commit est présent dans l’historique.

```bash
git log --online
```

Résultats :  
commit 8d5a76b6ac84304d58dd308a8873ea562a0c2c6c  
Author: cecile.vilport <cecile.vilport@3wa.fr>  
Date: Thu Oct 3 14:36:27 2024 +0200  

commit d6c1d66cf00a9bded1b39f714b0ef4dcbc992499 (HEAD -> main, origin/main)  
Author: Louis A <louis.appadourai@3wa.io>  
Date: Mon Jan 5 21:46:21 2026 +0100  

Ajout d'une quatrième image et d'un dot supplémentaire  

commit d94cb8658c116e4775a94395045a776fce1fcff5  
Author: cecile.vilport <cecile.vilport@3wa.fr>  
Date: Thu Oct 3 14:58:10 2024 +0200  

first commit

## 6 Gestion d’un conflit (taille des dots)

## 1 Modification sur GitHub
## On Modifiee css/style.css : dots 15px → 20px
## Commit directement sur GitHub

Résultats :

```css
.dot {
    cursor: pointer;
    height: 20px;
    width: 20px;
    margin: 0 2px;
    background-color: #bbb; border-radius: 50%;
    display: inline-block;
    transition: background-color 0.6s ease;
}
```

## 2 Modification locale
## On Modifie dans le CSS local : dots 15px → 25px
## On a fait un commit local différent de celui sur GitHub pour créer un conflit volontaire

## Vérifie l’état du dépôt

```bash
git status
```

## 7 Enregistrez vos modifications locales

```bash
git add css/style.css
```

## 8 Rapatrier la version distante → conflit
## git pull intègre les commits distants avant tes commits locaux
## Git détecte le conflit car le fichier CSS a été modifié à la fois localement et sur GitHub

```bash
git pull --rebase
```

Résultats(message Git indiquant le conflit) :

```txt
<<<<<<< HEAD
## Version locale
width: 25px;
height: 25px;

=======

>>>>>>> origin/main
## Version GitHub
width: 20px;
height: 20px;
```

## 8 Résolution du conflit
## On Ouvre css/style.css
## On Choisis la version finale (25px)
## On Supprimer les marqueurs <<<<<<<, =======, >>>>>>>

Résultats (CSS après résolution) :

```css
.dot {
    cursor: pointer;
    height: 25px;
    width: 25px;
    margin: 0 2px;
    background-color: #bbb;
    border-radius: 50%;
    display: inline-block;
    transition: background-color 0.6s ease;
}
```

## Indique à Git que le conflit est résolu

```bash
git add css/style.css
git commit -m "Résolution du conflit sur la taille des dots"
git push
```

## Vérification de l'historique des commits

```bash
git log --oneline
```

Résultats (Permet de vérifier l’ordre et le contenu des commits : L’ajout de la 4e image, La modification GitHub, La modification locale, La résolution du conflit) :  
8ae9203 (HEAD -> main, origin/main, origin/HEAD) Modification locale de la taille des dots à 25px  
8984a27 Style.css : modification de la taille des dots  
d6c1d66 Ajout d'une quatrième image et d'un dot supplémentaire  
d94cb86 first commit  
8d5a76b first commit
