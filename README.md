# Site web du festival Herbes Folles

Ce site est basé sur le générateur de site [Jekyll](http://jekyllrb.com) ainsi que le thème [Hitchens](https://github.com/patdryburgh/hitchens/).

Ce fichier 'README' est structuré en quatre parties :

1. Des mini-guides pour accomplir des tâches spécifiques
2. Une explication succinte du fonctionnement de ce site web
3. Une description des différents dossiers et de leur contenu
4. Un guide pour les personnes techniques souhaitant mettre en place le site web sur leur PC personnel afin de visualiser les modifications en temps réel

----


## Guide de survie en milieu technique hostile

Dans cette section vous trouverez différentes solutions à des besoins que vous pourriez avoir :

- changer des couleurs
- mettre à jour la page d'accueil
- mettre à jour le titre du site internet
- modifier le contenu d'une page
- mettre une image sur une page
- modifier le bandeau

### Je veux changer la couleur du site, c'est où ?

Les différentes couleurs sont définies dans les règles CSS.
Dans le fichier `_saas/variables.scss` vous trouverez différentes déclarations sous la forme :

```scss
$nom_de_variable : #000000;
```

Pour mettre à jour la couleur, modifiez la valeur en hexadécimal sans toucher au nom de la variable.

**Attention** : Cela modifie la couleur en question sur toutes les pages. Il n'est pas prévu de modifier une couleur uniquement sur une page.

### Je veux mettre à jour le contenu de la page d'accueil, ou le titre du site

La page d'accueil est fabriquée automatiquement à partir de la liste des posts de blog, et de deux fichiers de configuration.

Si vous voulez mettre à jour le texte de l'introduction, c'est via le fichier `_data/home.yml`.

Si vous voulez mettre à jour le titre, le sous-titre ou la description, c'est dans le fichier `_config.yml` les lignes :

```yaml
# Website content
title: Herbes Folles II
description: >- # this means to ignore newlines until "baseurl:"
  Les 19, 20 et 21 Août 2022
extended_description: >-
  Musique electronique, décoration et nourriture maison 
```

### Je veux changer le contenu d'une page

Deux options :

1. vous voulez changer le contenu d'un article 
2. vous voulez changer le contenu d'une page "standard"

Dans les deux cas, vous aurez besoin de connaître les bases de la syntaxe Markdown.
Voici donc des exemples de syntaxe markdown [ici](https://fr.wikipedia.org/wiki/Markdown#Exemples_de_syntaxe) et un guide [là](https://blog.wax-o.com/2014/04/tutoriel-un-guide-pour-bien-commencer-avec-markdown/).

#### 1 - Article

Allez modifier directement le contenu dans le fichier `_posts/<article>.md`.

#### 2 - Page standard

Allez modifier le contenu dans le fichier `content/<nom de la page>.md`

### Je veux mettre une image dans mon article/page

Déposer votre image dans le dossier `assets/images/`.

Dans votre page/article vous pouvez inclure votre image en utilisant la syntaxe :

```markdown
![Nom alternatif de l'image](/assets/images/<nom de mon image>)
```

Vous avez un exemple dans la page `content/charte.md`.

### Je veux modifier les pages ou les urls présentent dans le bandeau

La définition de la liste des pages du bandeau se trouve dans `_data/menu.yml`. La syntaxe du YAML peut sembler simple au premier abord, mais si vous avez un doute sur ce que vous faîtes, je vous recommande de lire cette page : [yaml syntaxe](https://docs.ansible.com/ansible/latest/reference_appendices/YAMLSyntax.html).

----

## Fonctionnement de Jekyll

L'idée centrale de cet outil, c'est de séparer le contenu (ce qu'on écrit dans les pages web), de la mise en forme (le HTML et le CSS utilisé pour afficher le contenu).

On a donc d'un côté le contenu du site écrit et mise en forme de manière minimale au format Markdown.

De l'autre côté, on a les règles de styles CSS qui vont spécifier la police, la couleur, etc.

Et au milieu, on retrouve des fichiers HTML qui servent de patron pour fabriquer les pages en fonction du contenu. Ce sont ces fichiers qui associent à du contenu, un ensemble de balises HTML et de classes CSS.

----

## Organisation des dossiers

Ce site web est fabriqué à partir de trois grandes catégories de fichiers :
- ceux qui portent le contenu du site, écrit au format Markdown (des exemples de syntaxe markdown [ici](https://fr.wikipedia.org/wiki/Markdown#Exemples_de_syntaxe), un guide [là](https://blog.wax-o.com/2014/04/tutoriel-un-guide-pour-bien-commencer-avec-markdown/))
- ceux qui définissent les règles de mise en forme, au format CSS
- ceux qui portent la structure du site avec un mélange de HTML et de YAML (pourquoi le yaml ? => pour rendre paramétrable le site)

### Contenu

On retrouve deux grands types de contenus :
- les pages 'standards', stockées dans le dossier `content`. En gros il s'agit du contenu qui n'est pas daté.
- les articles de blog, stockés dans le dossier `_posts`

Le maximum de contenu est écrit au format markdown. Si vous voulez comprendre un peu mieux l'en-tête présent sur les fichiers, [la documentation](https://jekyllrb.com/docs/posts/) contiens toutes les réponses :)

### Mise en forme (CSS)

Le dossier `_saas` contiens des fichiers de règles CSS. Ceux-ci sont dans une syntaxe un poil différente du CSS, puisque l'on peut notamment déclarer des variables (très pratique pour les couleurs !!!).

Si vous ne touchez qu'à la couleur, vous devriez pouvoir modifier seulement le fichier `_saas/_variable.scss`.

### Structure

Le dossier `_layouts` contiens les fichiers HTML permettant de transformer les pages au format markdown en fichiers HTML.

Il se base aussi sur le dossier `_includes` qui sers à définir des bouts de HTML qui sont réutilisés à travers plusieurs pages (par exemple `_includes/menu.html` contiens le code source du bandeau de menu).

La syntaxe de ces fichiers est un peu particulière. En effet, il s'agit de "patrons" qui sont ensuite remplis avec le contenu des fichiers Markdown. Il s'agit de la syntaxe Liquid ([doc](https://shopify.github.io/liquid/basics/introduction/))

Vous trouverez aussi des fichiers yml dans le dossier `_data` :
- `data/home.yml` : ce fichier définit le contenu de la page d'accueil
- `data/menu.yml` : ce fichier définit le contenu du bandeau de menu

----

## Faire tourner le site web en local

Les instructions suivantes sont plutôt valable pour un système **Linux** (désolé :|). Les blocs de codes indiquent des commandes à taper dans une console.

Commencez par installer le langage de programmation ruby (sur Ubuntu par exemple `apt install ruby`).

Puis, clonez ce repo :

```bash
git clone git@github.com:Herbes-Folles/Herbes-Folles.github.io.git
```

Installez *Jekyll* :

```bash
cd Herbes-Folles.github.io # On rentre dans le dossier du repo
bundle install # On installe jekyll
bundle exec jekyll serve # On démarre jekyll
```

Si tout s'est bien déroulé, visitez la page [http://127.0.0.1:4000/](http://127.0.0.1:4000/) sur votre navigateur et vous devriez vois le site d'herbe folles.

Le site est refabriqué/rechargé automatiquement à chaque modification (**/!\ sauf pour le fichier `_config.yml`**).


## License

The code for this theme is available as open source under the terms of the [MIT License](https://opensource.org/licenses/MIT).