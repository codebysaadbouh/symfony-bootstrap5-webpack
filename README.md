## Intégration de Webpack sur un projet Symfony et l'ajout de la nouvelle version 5 de bootstrap sur le projet

![symfony - bootstrap 5 - Webpack](https://photos.app.goo.gl/m8h1jZ4LLZq7XYUj9)
<br>

1 - Installer **Encore** : 

- `composer require symfony/webpack-encore-bundle`

<br>

2 - Installer les dépendances que nous avons sur notre package.json : 

- `npm install`

<br>
3 - Sur /assets nous allons voir de nouveaux fichiers : comme /styles/app.css et  app.js

<br>

> Nous allons modifier l'extension du fichier **app.css** et mettre à la place ***.scss** et le spécifier sur app.js. <br> Il faut aussi décommenter le .**enableSassLoader()** sur **webpack.config.js** qui se trouve sur la racine de notre projet symfony

<br>
4 - Installation de l'outil de compilation SASS et modification de base.html.twig

- `npm install sass-loader node-sass --save-dev`

> Pendant que ces packages s'installent nous allons modifier un peu le base.html.twig pour l'indiquer qu'on aura des feuilles de style et  des scripts compilés par webpack

```  
{% block stylesheets %}
    {{ encore_entry_link_tags('app') }}
{% endblock %}
{% block javascripts %}
    {{ encore_entry_script_tags('app') }}
{% endblock %}
```

> À la fin de cette étape je vous conseille de faire un 'npm run build' pour s'assurer que tout fonctionne bien

<br>
5 - Installation des requirements nécessaires pour la compilation de bootstrap

- `npm install postcss-loader autoprefixer --dev`

>   Nous allons du coup créer un fichier sur la racine de notre projet nommé : **postcss.config.js** et nous allons y copier le code ci-dessous pour lui expliquer qu'il doit charger l'autoprexifer

```
module.exports = {
    plugins: {
        autoprefixer : {}
    }
}
```

> À la fin de cette étape je vous conseille de faire un 'npm run build' pour s'assurer que tout fonctionne bien

<br>
6 - Installation de bootstrap : 

- `npm install bootstrap @popperjs/core`

> Importer le javascript de boostrap sur assets/app.js en ajoutant ce code ci-dessous  : 

```
import { Tooltip, Toast, Popover } from 'bootstrap';
```

> Nous allons créer sur assets/styles/ un fichier **costum.scss** (Pour faire de la customisation (overriding) sur le bootstrap par exemple ) 
> Dans le fichier **app.scss ** on va mettre les deux lignes d'importations à prendre en compte :

```
@import "custom";
@import "~bootstrap/scss/bootstrap";
```

> A la fin de cette étape je vous conseille de faire un 'npm run build' pour s'assurer que tout fonctionne bien et d'ajouter après sur base.html.twig l'element ci-dessous sur le \<head> :
```
<meta name="viewport" content="width=device-width, initial-scale=1.0">
```


### Concernant le test :

> Vous pouvez créer un nouveau controller  et d'y ajouter un contenu bootstrap, normalement tout devrait bien marcher. 

> Pour la costumisation je vous conseille de voir [la documentation de bootstrap](https://getbootstrap.com/docs/5.0/customize/sass/) qui assez explicite.

<br>
<br>

> Auteur :  Cheikh Saad Bouh SOW, analyste développeur
