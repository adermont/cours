# Configuration de Git

Préambule : la documentation complète de Git est ici : https://git-scm.com/book/fr/v2


## Qu'est-ce que c'est ?

Git est un **système de gestion de versions** (VCS) qui se comporte un peu comme 
une base de données dans laquelle on stocke toutes les versions de nos fichiers
sources.

Il est distribué sous forme d'un package de programmes à installer sur sa 
machine et qu'on peut ensuite utiliser en ligne de commande pour sauvegarder
l'historique de modification des fichiers texte.

Là où c'est puissant, c'est que Git est un système distribué. Il fonctionne en
local mais il est capable de gérer des fichiers situés sur une machine distante
et partagés par plusieurs utilisateurs du même réseau (que ce soit un réseau 
privé d'entreprise ou Internet).


## Comment ça fonctionne ?

**Cas d'utilisation n°1** : en local, juste pour vous

1. Vous créez un nouveau fichier java, markdown, html ...
2. Vous éditez votre fichier avec votre éditeur (IntelliJ, Notepad++ ...)
3. Quand vous avez fini la version `V1`, vous la publiez dans Git
4. Vous faites évoluer votre code
5. Vous publiez une seconde révision `V2`
6. Vous vous rendez compte qu'il y a une erreur :  
6.1 Vous consultez l'historique des versions dans Git  
6.2 Vous décidez de supprimer votre version V2
7. Vous repartez de la version V1 et modifiez votre code


**Cas d'utilisation n°2** : Référentiel partagé sur un serveur

1. Vous travaillez avec d'autres utilisateurs sur un projet GitHub ?
2. Clonez le repository du projet pour en avoir une copie locale
3. Vous faites des modifications sur un fichier
4. Vous publiez une nouvelle révision dans votre dépot Git local
5. Quand vous êtes prêt, vous envoyez vos modifications sur le repo GitHub
6. Un autre utilisateur met à jour son dépôt local et voit vos modifications


## Les versions et les commits

Une **version** (ou **révision**) est un **état du référentiel à un instant T**. 
C'est à dire **l'état de CHAQUE FICHIER**. (En fait Git ne sauvegarde pas 
entièrement les fichiers mais ne conserve que les différences entre 2 versions 
d'un fichier.)

Quand on a fini de travailler sur des fichiers, on les met dans la 
**staging area** puis on les publie avec `commit`. Ceci a pour effet créer une 
nouvelle version du référentiel dans la base de données Git.

Une fois qu'on a créé une version avec la commande `commit`, elle sera toujours 
disponible (à la condition de ne pas supprimer le répertoire caché `.git` à la 
racine de votre projet évidemment). On peut voir ça comme une sorte d'archivage.

Au fil du temps, on ne se souvient pas de toutes nos modifications et parfois il 
est utile d'aller voir dans l'historique d'un fichier QUI a travaillé dessus et 
CE QUI A ETE FAIT. Ca permet de mieux comprendre pourquoi l'application s'est 
mise à dysfonctionner subitement après un group de modifications.

Voici un schéma montrant plusieurs versions d'un référentiel Git :

[![](https://mermaid.ink/img/pako:eNqtkMFOhDAQhl-lGUN6IaQthYWeTbx4M_FguMxCgWaBErYYV8K7W1ld3URv27nM_P837XQWKG2lQUEQLGYwTpGF0M42j_pVd1QRWun93NCQUNfqXp-VGufOUfItPuNkcN_po3eXYiBXhzbGsc-2u7pGxhgN_yL4F1HXyT-EuBDIaDGsxEcQnElvP0w4tpe-stXlwc6O9GiGH9X2vXE3KX8lEEKvJ_9Q5be4fb-AbS0FKJ9WOB0K8AN7Dmdnn05DCcpNsw5hHit0-t5gM2EPqsbu6NURhxdrr2pQC7yB2vEoFyIWTGQ8Z1wmIZxACS6iVGZilzKexUks5RrC-3YDj3ga81RKnseSS2-vH2owiQ8?type=png)](https://mermaid.live/edit#pako:eNqtkMFOhDAQhl-lGUN6IaQthYWeTbx4M_FguMxCgWaBErYYV8K7W1ld3URv27nM_P837XQWKG2lQUEQLGYwTpGF0M42j_pVd1QRWun93NCQUNfqXp-VGufOUfItPuNkcN_po3eXYiBXhzbGsc-2u7pGxhgN_yL4F1HXyT-EuBDIaDGsxEcQnElvP0w4tpe-stXlwc6O9GiGH9X2vXE3KX8lEEKvJ_9Q5be4fb-AbS0FKJ9WOB0K8AN7Dmdnn05DCcpNsw5hHit0-t5gM2EPqsbu6NURhxdrr2pQC7yB2vEoFyIWTGQ8Z1wmIZxACS6iVGZilzKexUks5RrC-3YDj3ga81RKnseSS2-vH2owiQ8)

> Notez que dans Git, l'identifiant d'une version est un `hash`.

Un **commit** c'est donc l'action de créer une nouvelle version, un nouvel état
du référentiel contenant toutes les différences réalisées depuis la version 
précédente. 

> On parle aussi bien d'un `commit` pour désigner **l'action** de publier
une modification, que pour désigner la **nouvelle version** obtenue par cette
publication.


### Les tags

Un tag est comme une photo de l'état d'un repository à un instant T. Il s'agit
cependant d'un commit normal sur qu'on peut utiliser comme source d'une nouvelle
branche.

Par exemple pour livrer une version stable au client, on pose un **tag**
(ou "étiquette", par ex. : "`VERSION_CLIENT_2023-01-12`") sur le commit qui sert 
de référence pour cette livraison. (Par la suite, si on doit travailler sur 
cette version, pour corriger un bug bloquant par exemple, il suffit de 
`checkout` le *commit* correspondant au tag et de créer une branche partant de 
ce *commit*.)


## Les branches

Les branches sont un moyen d'organiser le travail entre plusieurs personnes.
Chaque développeur.euse travaille en général dans une branche séparée du projet
afin de ne pas impacter le travail des autres lorsqu'il/elle publie ses modifications
sur le serveur.

> **NOTE** : bien qu'une branche contienne l'ensemble des fichiers et répertoires 
d'un projet, ce n'est qu'une simple information dans la base de données Git. C'est
à dire que physiquement, vos fichiers ne sont pas dupliqués sur le disque à chaque 
fois que vous créez une branche.

Il est important d'apprendre à travailler avec les branches et de savoir passer
d'une branche à une autre. Par exemple pour résoudre un bug trouvé en production, 
il faudra créer une branche spécialement pour résoudre ce bug. Pourquoi ? 
La réponse tient en 2 points :

- D'abord le fait de créer une branche vous permet de **travailler sereinement**
puisque vous n'avez pas d'impact sur la branche principale qui sert à produire
la version livrée au client. Donc moins de pression en cas d'erreur.

- Ensuite, quand vous créez une nouvelle branche, vous devez indiquer à partir
de quelle version du projet cette branche doit partir. Vous pourrez donc repartir
de la version **exacte** à laquelle correspond le bug que vous devez résoudre, 
au lieu de repartir de votre version courante qui peut embarquer un lot d'évolutions 
qui peuvent modifier le comportement de l'application et masquer le bug.

Voici un exemple de branches où on voit une branche 'main' qui sert à livrer
l'application au client et deux branches créées pour développer de nouvelles
fonctionnalités expérimentales :

[![](https://mermaid.ink/img/pako:eNqVU11rwjAU_SvhDslLkSSN1eZ5oAPflD2Mwri2aS32Q2oqc8X_vlSns6hMWwrt-bjnXEgbCMtIg4Jer0mL1CjSEJqVyVRvdUYVoZFe1Al1CDVLnesjEmOdGUpO4DtWKS4yvbFsExSkc9EkNay1vcQxMsaoc0vBfxVxPLijEGcFMhoUe2LvXu-otPS4wvXy7AuXOlyVtSE5psUfWuZ5akgaKRLAlgdwhxEXzKLCIlySWKOpK82vE66Zziz3MuWBVvKW_iqj20rcdYg7KYMnW3kPtep6hv9m5LpK9HnMyTcKgBhM2vfpfPYpmHAZb7HdWisyeRtPpvaZP72z_-TOnLUGcMDWtLLI_iOHwx3A4dAH0KoirFatbG91WJtytitCUKaqtQP1OkKjX1NMKsxBxZhtLLrG4qMsO9-gGvgCNeR9XwjXLjziPuNy4MAOlOCi78mRGHqMj9yBK-Xege_DBN7nnss9KbnvSi4tvf8BuAUX9w?type=png)](https://mermaid.live/edit#pako:eNqVU11rwjAU_SvhDslLkSSN1eZ5oAPflD2Mwri2aS32Q2oqc8X_vlSns6hMWwrt-bjnXEgbCMtIg4Jer0mL1CjSEJqVyVRvdUYVoZFe1Al1CDVLnesjEmOdGUpO4DtWKS4yvbFsExSkc9EkNay1vcQxMsaoc0vBfxVxPLijEGcFMhoUe2LvXu-otPS4wvXy7AuXOlyVtSE5psUfWuZ5akgaKRLAlgdwhxEXzKLCIlySWKOpK82vE66Zziz3MuWBVvKW_iqj20rcdYg7KYMnW3kPtep6hv9m5LpK9HnMyTcKgBhM2vfpfPYpmHAZb7HdWisyeRtPpvaZP72z_-TOnLUGcMDWtLLI_iOHwx3A4dAH0KoirFatbG91WJtytitCUKaqtQP1OkKjX1NMKsxBxZhtLLrG4qMsO9-gGvgCNeR9XwjXLjziPuNy4MAOlOCi78mRGHqMj9yBK-Xege_DBN7nnss9KbnvSi4tvf8BuAUX9w)


- On voit sur ce graphe que la branche `feature1` démarre à partir de la 
version `v2` de la branche `main`. La branche `feature2` démarre elle-même
à partir de la version `v3` de la branche `feature1`.

- Il y a eu 2 commits dans la branche `feature1` puis elle a été fusionnée
dans la branche `main`. La version `v8` ainsi créée a été tagguée "LTS_202301"
et il s'agit probablement d'une version livrée au client.

- La branche `feature` quant à elle est actuellement en version `v9` et 
continue son développement.



## Travail à faire :

- Suivez le tutoriel [configuration_git.pdf](https://github.com/adermont/cours/blob/main/git/configuration_git.pdf)
  pour installer Git sur votre machine et configurer SSH si ce n'est pas déjà fait.

- Suivez le tutoriel [Travailler avec GitHub](tuto_git_binomotron.md) pour publier 
votre projet "Binomotron" dans votre repository GitHub (ou pour synchroniser votre
repository avec votre dossier de projet local).

- Formez-vous (avec "Git it!" de préférence, il est bien pensé) :

   - [Git it!](https://github.com/jlord/git-it-electron) (tutos en anglais 
   + traduction en français, contient des commandes à taper dans un Terminal)
 
   - ou sinon [Git-Katas](https://github.com/eficode-academy/git-katas) (tutos en 
   anglais, contient des commandes à taper dans un Terminal)
   
   - ou encore [Oh my Git!](https://ohmygit.org) (format jeu vidéo, en anglais)

- Lisez [Git avec IntelliJ](https://www.jetbrains.com/idea/guide/tutorials/creating-a-project-from-github/)