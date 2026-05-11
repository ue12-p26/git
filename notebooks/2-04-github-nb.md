---
jupytext:
  text_representation:
    extension: .md
    format_name: myst
kernelspec:
  display_name: Calysto Bash
  language: bash
  name: calysto_bash
language_info:
  name: bash
  help_links:
  - text: MetaKernel Magics
    url: https://metakernel.readthedocs.io/en/latest/source/README.html
---

# github

+++

## c'est quoi ?

jusqu'ici on a vu le socle de git

mais on n'a encore rien dit sur github (ou gitlab ou bitbucket...) qui est un service qui va **au delà** du système git à proprement parler

pour ajouter **une dimension sociale** et offrir des possibilités de collaboration avec .. la terre entière !

+++

## les noms

* chaque **compte** a un nom unique (votre identifiant github par exemple), et  
  on peut ranger autant de repos qu'on veut dans cet espace

* on peut aussi créer des **organisations** (`ue12-p26` par exemple)  
  et pareil, dans une organisation on peut mettre autant de repos qu'on veut

* que ce soit dans un compte ou une orga, l'URL d'un repo est toujours de la forme  
  ***https://github.com/le-compte-ou-l-orga/le-nom-du-repo***  
  comme par exemple, pour ce cours justement:  
  `https://github.com/ue12-p26/git`  
  (ou encore, `git@github.com:ue12-p26/git.git` avec ssh)

`````{admonition} le remote *origin*
:class: dropdown note

toujours au sujet des noms, vous pouvez noter que le plus souvent,
si vous avez dans votre repo local un *remote* qui s'appelle `origin`, 
avec nos pratiques le plus souvent ce remote correspond au repo sur github:

```bash
  # pour lister les remotes
$ git remote
origin
  # pour voir à quelle URL correspond le remote 'origin'
$ git remote get-url origin
git@github.com:ue12-p26/git.git
```

````{admonition} créer un alias
:class: dropdown seealso

si comme moi vous avez du mal à retenir cette dernière commande, 
c'est le moment de vous créer un alias: 
``` bash
git config --global alias.url "remote get-url origin"
```
après quoi il vous suffira de faire
``` bash
$ git url
git@github.com:ue12-p26/git.git
```

````
`````

+++

## les accès

* signalons aussi que chaque repo peut être **public** ou **privé**  
  pour la suite, si on ne précise rien, ce sera pour parler de repos publics

* un repo public peut être  
  - **lu**, et donc aussi cloné, par tout le monde  
  - **écrit** (ou pourra pousser dedans) par une liste finie de gens définie dans les *Settings* du repo (et de l'orga)

* un repo privé quant à lui peut être  
  - **lu** et **écrit** par une liste finie de gens (idem)

+++

## le workflow usuel

### Alice publie du code

dans un scénario typique:
1. Alice commence à écrire un bout de code - appelons-le `rhubarbe` - sur son ordi  
  tout au long du codage, elle le met dans un repo git
1. lorsqu'elle est contente elle va "mettre cela sur github"  
  c'est-à-dire créer un repo vide dans `https://github.com/alice/rhubarbe`  
  et **pousser** son repo dedans [voyez aussi plus bas](#label-github-create-repo)
1. son travail devient donc accessible à tout le monde, et Bob le remarque
1. il télécharge alors le contenu du repo sur son ordi
  avec un `git clone`

+++

### d'autres gens s'en servent: les *Issues*

5. les gens qui utilisent le logiciel ont à leur disposition (dans le repo d'Alice) un espace qui s'appelle ***Issues***
1. dans lequel ils peuvent remercier Alice, poser des questions, signaler des soucis  
   et de manière générale discuter librement autour du projet  
   c'est le premier outil de la dimension sociale de ces plateformes collaboratives  
   ça se passerait dans `https://github.com/alice/rhubarbe/issues`

+++

### Bob modifie le code pour ses besoins

7. à ce stade Bob a tout sur son ordi, il peut modifier ce qu'il veut...
1. toujours en utilisant git bien sûr, il n'a pas besoin de l'avis ni de l'autorisation d'Alice pour créer des commits, c'est tout de même son ordi

+++

### Bob veut soumettre ses changements à Alice : le Fork

9. là par contre ça se corse un peu  
   il faut prendre en compte le fait que, si ça se trouve, Alice n'a jamais entendu parler de Bob et ignore même jusqu'à son existence !  
   du coup, pour commencer, Bob ne fait pas partie des gens qui ont le droit de modifier le repo d'Alice
1. pour contourner ça, et pour pouvoir a minima exposer son idée à Alice, Bob va se **créer un fork**  
   un *fork*, c'est tout simplement, **encore un clone** du repo, mais cette fois dans l'espace de Bob,  
   donc dans `https://github.com/bob/rhubarbe`
1. et la différence c'est que cette fois, **Bob a le droit** d'écrire dans ce *fork*
   il peut donc pousser ses nouveaux commits dans ce *fork* repo

+++

### Bob veut soumettre ses changements à Alice : le PR

12. mais ça n'est pas exactement suffisant, car à ce stade Alice n'a toujours aucune connaissance de l'existence de Bob, ni a fortiori de nouveaux commits
1. pour se manifester, Bob va créer ce qu'on appelle un ***PR*** (pour *Pull Request*)
   qui se trouvent ici `https://github.com/alice/rhubarbe/pulls`
1. ce PR est créé **dans le repo d'Alice** en indiquant  
   ￮ où se trouvent les changements proposés (typiquement en indiquant le fork de Bob, et accessoirement dans quelle branche)  
   ￮ et la branche dans le repo d'Alice où on propose de merger les nouveaux commits
1. dans ce PR va se nouer une discussion entre les deux protagonistes
   Alice peut soit refuser complètement, soit accepter tel quel, ou bien le plus souvent demander quelques modifications  
1. pendant cette discussion Bob continue à écrire dans son repo, pour tenir compte des demandes d'Alice
1. enfin, si/quand on arrive à un accord, Alice peut en un clic merger les changements de Bob dans son propre repo  
1. du coup les modifications de Bob profitent à tout le monde  
   et Bob n'a plus besoin de s'embêter à gérer sa version custom de `rhubarbe`  
   et là Bob est très content 🙂
1. et Alice aussi 🙂  
   parce que d'autres peuvent de cette manière la décharger de certains aspects du projet

+++

## quelques indices sur l'UI de github

+++

(label-github-create-repo)=
### créer un repo sur github: avec ou sans fichiers ?
:::::{admonition} 
:label: 
:class: tip

c'est sans doute l'occasion d'une petite digression, pour expliquer un problème fréquent avec les débutants

::::{grid} 2
:::{div}
lorsque vous allez sur github pour créer un repo, on vous pose quelques questions; et celles qui sont entourées en rouge ici à droite appellent un avertissement:

notamment **si vous avez déjà créé** un dépôt sur votre ordi, **ne cochez aucune de ces cases !**  
(ou pour le dire autrement, demandez à github de ne créer aucun fichier)

si vous le faites, cela oblige github à **créer un premier commit** (avec le contenu des fichiers que vous avez demandés)

:::

:::{image} media/github-create-repo-1.png
:size: 200px
:align: right
:::
::::
et pourquoi est-ce un problème si vous avez déjà des commits ?  
eh bien vous allez vous retrouver à devoir *merge* deux commits (celui de votre ordi et celui de github) qui n'ont **pas d'ancêtre commun**; et cela demande de recourir à des options spéciales

alors bon, oui c'est faisable (comme tout avec `git`), mais ça faire perdre du temps; et surtout ça donne un démarrage de projet qui ne ressemble à rien, avec deux racines sans parent, bref **c'est à éviter** !

::::{admonition} petit quiz: les recettes magiques affichées par github après création 
:class: dropdown note
d'ailleurs voici ce que vous montre github juste après que vous ayez créé un repo  
est-ce que vous arrivez à lire et à comprendre ce code ?
:::{image} media/github-create-repo-2.png
::::
:::::

+++

### pour créer un fork

il faut aller dans la page du repo sur github, et cliquer sur le bouton *Fork* en haut à droite

  ```{image} media/github-howto-fork.png
  :align: center
  :width: 600px
  ```

+++

### pour inviter des gens dans un repo

passer par l'onglet *Settings* comme ceci  
```{image} media/github-collaborators.png
:align: center
:width: 600px
```

+++

## `gh` (avancés)

enfin pour les avancés, sachez que toutes les opérations que l'on fait depuis l'interface web peuvent aussi être faits par la ligne de commande en utilisant un outil qui s'appelle `gh`  
voici par exemple comment je crée un repo pour le TP "class-ids" de mon groupe

```bash
$ gh repo create --public ue12-p26/git-tp-class-ids-groupe4
✓ Created repository ue12-p26/git-tp-class-ids-groupe4 on GitHub
```
