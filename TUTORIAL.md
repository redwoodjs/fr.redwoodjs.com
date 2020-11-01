# Bienvenue chez Redwood

Bienvenue chez Redwood! Si vous ne l’avez pas encore fait, prenez le temps de lire [Redwood README](https://github.com/redwoodjs/redwood/blob/main/README.md) pour en savoir un peu plus sur les origines de Redwood et les problèmes qu'il entend résoudre. Redwood assemble plusieurs technologies de façon inédite et qui correspond à ce que nous pensons être le futur des applications web avec base de données.  

Dans ce didacticiel, nous allons construire un moteur de blog. En réalité, un blog n’est probablement pas le candidat idéal pour une application construite avec Redwood: les articles peuvent être enregistrés dans un CMS et générées statiquement sous la forme de fichiers HTML servis par un CDN. Ceci étant, la plupart des développeurs comprennent intuitivement ce que recouvre ce type d’application, et un blog présente toutes les caractéristiques que nous souhaitons mettre en lumière. Nous avons donc décidé d'en construire un malgré tout.

Peut-être souhaitez-vous voir ce didacticiel en vidéo? C’est ici :

<div class="relative pb-9/16">
  <iframe class="absolute inset-0 w-full h-full" src="https://www.youtube.com/embed/tiF9SdM1i7M?rel=0" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture; modestbranding; showinfo=0" allowfullscreen></iframe>
</div>

<div class="relative pb-9/16 mt-4">
  <iframe class="absolute inset-0 w-full h-full" src="https://www.youtube.com/embed/SP5vbsWf5Yg?rel=0" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture; modestbranding; showinfo=0" allowfullscreen></iframe>
</div>

<div class="relative pb-9/16 mt-4">
  <iframe class="absolute inset-0 w-full h-full" src="https://www.youtube.com/embed/eT7iIy0F8Tk?rel=0" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture; modestbranding; showinfo=0" allowfullscreen></iframe>
</div>

<div class="relative pb-9/16 mt-4">
  <iframe class="absolute inset-0 w-full h-full" src="https://www.youtube.com/embed/UpD3HyuZkvY?rel=0" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture; modestbranding; showinfo=0" allowfullscreen></iframe>
</div>

## Prérequis

Ce didacticiel suppose que vous soyez déjà familier avec quelques concepts fondamentaux :

- [React](https://reactjs.org/)
- [GraphQL](https://graphql.org/)
- [The Jamstack](https://jamstack.org/)

Vous pouvez tout à fait compléter ce didacticiel sans savoir quoique ce soit sur ces technologies, mais il est possible que vous soyez un peu perdu par certains termes que nous utiliserons sans forcément les expliquer au préalable. D'une façon générale, il est toujours utile de savoir où se situe les frontières et pouvoir distinguer par exemple ce qui provient de React de ce qui est ajouté par Redwood. 

### Node.js et Yarn

Pendant l’installation, RedwoodJS commence par verifier si votre système possède les versions requises de Node et Yarn :

- node: ">=12"
- yarn: ">=1.15"

👉 **Important:** Si votre système ne repond pas à ces prérequis, _l’installation se soldera par une ERREUR._ Vérifiez en exécutant les commandes suivantes dans un terminal:

```
node --version
yarn --version
```
Procédez aux mises à jour le cas échéant, puis relancez l’installation de RedwoodJS lorsque vous êtes prêt !


> **Installer Node et Yarn**
>
> Il y a différentes façons d’installer Node.js et Yarn. Si vous procédez à leur installation pour la première fois, nous vous recommandons de suivre les points suivants :
>
> **Yarn**
>
> - Nous recommandons de suivre les instructions fournies sur [Yarnpkg.com](https://classic.yarnpkg.com/en/docs/install/).
>
> **Node.js**
>
> - Pour les utilisateurs de **Linux** et **Mac**, `nvm` est un excellent outil pour gérer plusieurs versions de Node sur un même système. Il demande un petit effort à mettre en place. Dans les deux cas, utiliser la version la plus récente de [Nodejs.org](https://nodejs.org/en/) fonctionne très bien.
>   - Pour les utilisateurs de **Mac**, si vous avez dejà installé Homebrew, vous pouvez l’utiliser pour [installer `nvm`](https://formulae.brew.sh/formula/nvm). Dans le cas contraire, suivez les [instructions d'installation pour `nvm`](https://github.com/nvm-sh/nvm#installing-and-updating).
>   - Pour les utilisateurs de **Linux**, vous pouvez suivre les [instructions d'installation pour `nvm`](https://github.com/nvm-sh/nvm#installing-and-updating).
> - Nous recommandons aux utilisateurs de **Windows** de visiter [Nodejs.org](https://nodejs.org/en/) pour savoir comment procéder.
>
> Si vous êtes un peu perdu au moment de choisir quelle version de Node utiliser, nous vous recommandons la plus récente LTS avec un numéro de version pair, actuellement il s'agit de la v12.

## Installation & Démarrage du développement

Nous utiliserons yarn ([yarn](https://yarnpkg.com/en/docs/install) est un pré-requis) pour créer la structure de base pour notre application :

    yarn create redwood-app ./redwoodblog

Vous obtenez ainsi un nouveau répertoire `redwoodblog` contenant plusieurs sous-répertoires et fichiers. Déplacez-vous dans ce répertoire, puis lancez le serveur de développement :

    cd redwoodblog
    yarn redwood dev

Votre navigateur web devrait se lancer automatiquement et ouvrir `http://localhost:8910` laissant apparaître la page d’accueil de Redwood. 

![Redwood Welcome Page](https://user-images.githubusercontent.com/300/73012647-97a43d00-3dcb-11ea-8554-42df29c36e4a.png)

> Mémoriser le numéro de port est très simple, comptez simplement: 8-9-10!

### Premier Commit

Maintenant que nous avons le squelette de notre application Redwood, c'est le bon moment pour enregistrer notre travail avec un premier commit... au cas où.

    git init
    git add .
    git commit -m 'Premier commit'

## Structure d'une application Redwood

Examinons maintenant les fichiers et répertoires qui ont été créés pour nous (laissons de côté les fichiers de configuration sur lesquels nous reviendrons plus tard)

```terminal
├── api
│   ├── prisma
│   │   ├── schema.prisma
│   │   └── seeds.js
│   └── src
│       ├── functions
│       │   └── graphql.js
│       ├── graphql
│       ├── lib
│       │   └── db.js
│       └── services
└── web
    ├── public
    │   ├── README.md
    │   ├── favicon.png
    │   └── robots.txt
    └── src
        ├── Routes.js
        ├── components
        ├── index.css
        ├── index.html
        ├── index.js
        ├── layouts
        └── pages
            ├── FatalErrorPage
            │   └── FatalErrorPage.js
            └── NotFoundPage
                └── NotFoundPage.js
```
Au premier niveau nous avons deux répertoires, `api` et `web`. Redwood sépare le backend (`api`) et le frontend (`web`) au sein du projet. ([Yarn qualifie cette séparation de "workspaces"](https://yarnpkg.com/lang/en/docs/workspaces/). Avec Redwood, on fait plutôt référence aux "côtés" web et api de l'application). Ainsi, lorsque plus tard vous serez amené à ajouter des packages, il vous faudra préciser dans quel côté ils doivent aller. Par exemple, (inutile d'exécuter ces commandes):

    yarn workspace web add marked
    yarn workspace api add better-fs

### Le Répertoire /api

A l'intérieur du répertoire `api` se trouve deux sous-répertoires :

- `prisma` contient du code d'infratructure relatif à la base de donnée

  - `schema.prisma` contient le schéma de la base de données (ses tables et ses colonnes)
  - `seeds.js` est utilisé pour initialiser la base de données avec les données de base nécessaire à votre application (utilisateur admin, configuration diverses..).

  Lorsque nous aurons créé notre première table dans la base de données, nous trouverons également à cet endroit une base de données SQLite sous la forme d’un fichier `dev.db`, ainsi qu’un répertoire `migrations` contenant des captures successives du schéma au fil de son évolution.

- `src` contient l'ensemble du code côté backend. `api/src` contient quatre répertoires supplémentaires :
  - `functions` contiendra toutes les [fonctions lambda](https://docs.netlify.com/functions/overview/) utilisées par votre application en plus du fichier `graphql.js` généré automatiquement par Redwood. Ce dernier fichier est requis pour utiliser une API GraphQL.
  - `graphql` contient votre schéma GraphQL écrit au format SDL (Schema Definition Language). Les fichiers SDL se terminent par `.sdl.js`.
  - `lib` contient un seul fichier, `db.js`, qui instancie le client Prisma utilisé pour dialoguer avec la base de données. Vous pouvez parfaitement personnaliser ce fichier en ajoutant des options supplémentaires. Vous pouvez utiliser ce répertoire pour tout code relatif au côté API de votre application qui ne trouverai pas sa place dans `functions` ou `services`.
  - `services` contient la logique métier de votre application. Lorsque vous effectuez une requête ou une mutation de données via GraphQL, ce code se trouve ici dans un format réutilisable depuis d’autres endroits de votre application.

Et nous en avons terminé avec la partie backend.

### Le répertoire /web

- `src` contient plusieurs sous-répertoires :
  - `components` contient vos composants React traditionnels ainsi que les _Cells_ introduites par Redwood (nous y reviendrons bientôt en détail).
  - `layouts` contient du code HTML sous forme de composants qui viennent entourer le contenu de votre application et sont partagés par les différentes _Pages_.
  - `pages` contient des composants souvent insérés dans les _Layouts_ et qui constituent les points d'entrées de votre application pour une URL donnée (une URL comme `/articles/hello-world` correspondra ainsi à une page tandis que `/contact-us` correspondra à une autre page). Chaque nouvelle application comprend deux pages par défaut :
    - `NotFoundPage.js` qui est utilisée lorsqu’aucune route n’est trouvée par le routeur (voir `Routes.js` plus bas).
    - `FatalErrorPage.js` qui est utilisée lorsqu’une erreur survient, qu’elle n’a pas été gérée, et qu’il n’est pas possible de poursuivre plus avant sans faire exploser l’application (en général il s’agit d’une page blanche).
- `public` contient des ressources non utilisées par vos composants React (En bout de chaîne, ces ressources seront copiées sans être modifiées dans le répertoire racine de l’application finale):
  - `favicon.png` est l’icône utilisée par les onglets des navigateurs lorsqu’une page est ouverte (par défaut il s’agit du logo RedwoodJS).
  - `robots.txt` est utilisé pour controller ce que les moteurs de recherche sont [autorisé à indexer](https://www.robotstxt.org/robotstxt.html).
  - `README.md` explique comment, et quand, utiliser le répertoire `public` pour vos ressources statiques. Il mentionne également les bonnes méthodes pour importer des ressources à l'intérieur des composants via Webpack. Vous pouvez également lire à ce sujet ce [fichier README.md sur GitHub](https://github.com/redwoodjs/create-redwood-app/tree/main/web/public).
- `index.css` est l'endroit par défaut où placer vos règles CSS. Il existe cependant d’autres possibilités avancées.
- `index.html` est le point d’entrée React standard de votre application.
- `index.js` contient le code de démarrage pour une application Redwood.
- `Routes.js` contient les définitions des routes de l’application afin de faire correspondre chaque URL à une _Page_.

## Notre Première Page

Donnons à nos utilisateurs quelque chose de plus à contempler que la page d'accueil de Redwood. Utilisons la commande `redwood` pour créer une première page :

    yarn redwood generate page home /

Cette commande fait les choses suivantes :

- Création de `web/src/pages/HomePage/HomePage.js`. Redwood prend le nom spécifié comme premier argument, le met en majuscules et le suffixe avec "Page" pour construire votre nouveau composant de type Page.
- Création d’un fichier de test du composant `web/src/pages/HomePage/HomePage.test.js` avec un simple test d’exemple à l’intérieur. Vous écrivez _toujours_ les tests de vos composants, _n’est-ce pas ??_
- Création d’un fichier Storybook `web/src/pages/HomePage/HomePage.stories.js`. Storybook est un outil formidable pour développer efficacement et organiser vos composants. Si vous souhaitez en savoir plus jetez un oeuil à ce [sujet sur le forum Redwood](https://community.redwoodjs.com/t/how-to-use-the-new-storybook-integration-in-v0-13-0/873) pour apprendre comment l’utiliser.
- Ajout d’une `<Route>` dans `web/src/Routes.js` qui fait correspondre le chemin `/` à la nouvelle page _HomePage_.

> **Import automatique des pages dans le fichier Routes**
>
> Si vous regardez dans Routes, vous constaterez mention d'un composant, `HomePage`, qui n'est présent nulle part ailleurs. Redwood importe automatiquement toutes les pages dans le fichier Routes puisque nous aurons besoin de toutes les référencer de toute façon. Cela permet de s'épargner un `import` massif qui viendrait encombrer le fichier Routes.

En réalité, cette page est déjà active (et votre navigateur l’a rechargée pour vous) :

![Default HomePage render](https://user-images.githubusercontent.com/300/76237559-b760ba80-61eb-11ea-9a77-b5006b03031f.png)

D’accord, ça ne flatte pas encore la rétine mais c’est un début! Ouvrez cette page dans votre éditeur, modifiez un peu le texte et sauvegardez. Votre navigateur devrait recharger la page avec vos modifications.

### Routing

Ouvrez `web/src/Routes.js` et observez la route qui vient d’être créée :

```html
<Route path="/" page={HomePage} name="home" />
```

Essayez de modifier cette route de la façon suivante:

```html
<Route path="/hello" page={HomePage} name="home" />
```

Dès que vous ajoutez votre première route, la page d'accueil par défaut de Redwood disparaît. Désormais, lorsqu'aucune route ne peut être trouvée pour l'URL demandée, Redwood va retourner la page `NotFoundPage`. Modifiez l'URL de votre navigateur pour ouvrir `http://localhost:8910/hello`, vous devriez voir de nouveau le contenu de `HomePage.js`.

Modifiez à nouveau la route pour revenir à son état initial `/` avant de continuer. 

## Une Seconde Page et un Lien

Ajoutons donc une page "About" à notre blog de manière à ce que personne n'ignore qui se trouve derrière cette application exceptionnelle. Nous allons créer une nouvelle page en utilisant `redwood`:

    yarn redwood generate page about

Remarquez que nous n'avons pas spécifié de chemin cette fois-ci, uniquement le nom de la page. En effet, si vous ne le précisez pas, la commande `redwood generate page` créera une `Route` en lui donnant pour chemin le nom de la page préfixé par un slash `/`. Dans le cas présent, ce sera donc `/about`. 

> **Fragmenter le code pour chaque page**
>
> Au fur et à mesure que vous ajoutez des pages à votre application, vous pouvez légitimement vous inquiéter du fait que le navigateur va devoir télécharger un volume initial de données toujours croissant. Soyez rassuré! Redwood va automatiquement fragmenter le code pour chaque page de telle façon que le chargement soit toujours extrêmement véloce. Vous pouvez donc créer autant de pages que vous le souhaitez sans vous inquiéter outre mesure de la taille finale du bundle webpack. Si, dans le cas contraire, vous souhaitez que certaines pages soient spécifiquement intégrées dans le bundle principal, il vous est possible de personaliser cette fonctionalité.

`http://localhost:8910/about` devrait maintenant pointer sur votre nouvelle page. Bien entendu, absolument personne ne va trouver cette page de votre blog en modifiant manuellement l'URL! Ajoutons donc un lien depuis la page d'accueil vers la page About, et vice-versa. Nous commencerons par créer un simple header et une barre de navigation dans `HomePage.js`:

```javascript{3,7-19}
// web/src/pages/HomePage/HomePage.js

import { Link, routes } from '@redwoodjs/router'

const HomePage = () => {
  return (
    <>
      <header>
        <h1>Redwood Blog</h1>
        <nav>
          <ul>
            <li>
              <Link to={routes.about()}>A Propos</Link>
            </li>
          </ul>
        </nav>
      </header>
      <main>Home</main>
    </>
  )
}

export default HomePage
```

Remarquons ici plusieurs points :

- Redwood adore les "[Function Components](https://www.robinwieruch.de/react-function-component)". Nous ferons un usage fréquent des "[React Hooks](https://reactjs.org/docs/hooks-intro.html)" au fil de l'élaboration de notre blog, et ces derniers ne sont actifs que dans les "function components". Vous êtes libres d'utiliser des "class components", mais nous vous recommandons de les éviter sauf cas particulier.
- Les balises Redwood `<Link>`, dans leur usage le plus simple, prennent un seul attribut `to`. Cet attribut `to` appelle une "_named route function_" de façon à générer l'URL correcte. Cette fonction possède le même nom que l'attribut `name` présent sur la `<Route>`:

  `<Route path="/about" page={AboutPage} name="about" />`

  Si vous n'aimez pas le nom que la commande `redwood generate` utilise pour votre route, vous pouvez parfaitement le changer dans le fichier `Routes.js`! Les routes nommées sont extrêmement utiles car, si vous désirez modifiez le chemin associé avec une route, il vous suffit de le modifier dans le fichier `Routes.js` et immédiatement tous les liens qui utilisent cette route pointerons au bon endroit. Vous pouvez également passer directement une chaîne de caractères à l'attribut `to`, mais alors vous ne bénéficiez plus de ce mécanisme bien utile. 

### Retour à la maison

Une fois sur la page "About", nous n'avons aucun moyen de revenir en arrière. Pour y remédier, ajoutons également un lien à cet endroit:

```javascript{3,7-25}
// web/src/pages/AboutPage/AboutPage.js

import { Link, routes } from '@redwoodjs/router'

const AboutPage = () => {
  return (
    <>
      <header>
        <h1>Redwood Blog</h1>
        <nav>
          <ul>
            <li>
              <Link to={routes.about()}>About</Link>
            </li>
          </ul>
        </nav>
      </header>
      <main>
        <p>
          Ce site est créé avec pour seule intention de démontrer la puissance créative de Redwood! Oui, c'est très 
          impressionant :D
        </p>
        <Link to={routes.home()}>Retour à la page d'accueil</Link>
      </main>
    </>
  )
}

export default AboutPage
```

Bien! Affichons cette page dans le navigateur and vérifions que nous pouvons aller et venir entre les différentes pages.

En tant que développeur de classe cosmique, vous avez probablement repéré ce copier-coller un peu lourd du `<header>`. Nous aussi. C'est la raison pour laquelle Redwood dispose d'un petite chose bien pratique appelé "_Layout_"."

## Layouts

Une façon de résoudre la duplication du `<header>` aurait pu être de créer un composant `<Header>` et l'inclure à la fois dans `HomePage` et `AboutPage`. C'est valide! Mais il y a beaucoup mieux... Dans l'idéal, votre code ne devrait comporter qu'une seule et unique balise `<header>`.

Lorsque vous regardez à ces deux pages, quelle est leur raison d'être principale? Toutes deux ont un peu de contenu à afficher. Toutes deux ne devraient pas avoir à connaître ce qui vient avant ce contenu (comme un `<header>`), ou après ce même contenu (comme un `<footer>`). C'est exactement ce que font les "Layouts": ils entourent une page dans un composant qui va ensuite afficher à l'intérieur le contenu de la page:

<img src="https://user-images.githubusercontent.com/300/70486228-dc874500-1aa5-11ea-81d2-eab69eb96ec0.png" alt="Diagramme de structure des Layouts" width="300">

Utilisons Redwood pour générer un layout contenant ce `<header>` :

    yarn redwood g layout blog

> **raccourci `generate`**
>
> Désormais nous utiliserons le raccourci `g` à la place de `generate`

Ce faisant, nous avons créé le fichier `web/src/layouts/BlogLayout/BlogLayout.js` et un son fichier de test associé. Nous appellerons ce dernier le "blog" layout car nous aurons certainement d'autres layout plus tard (un layout "admin" par exemple).

Supprimez ce `<header>` de `HomePage` et `AboutPage` et copier son contenu à l'intérieur du layout. Supprimons également le doublon de la balise `<main>` par la même occasion.

```javascript{3,7-19}
// web/src/layouts/BlogLayout/BlogLayout.js

import { Link, routes } from '@redwoodjs/router'

const BlogLayout = ({ children }) => {
  return (
    <>
      <header>
        <h1>Redwood Blog</h1>
        <nav>
          <ul>
            <li>
              <Link to={routes.about()}>About</Link>
            </li>
          </ul>
        </nav>
      </header>
      <main>{children}</main>
    </>
  )
}

export default BlogLayout
```

`children` est l'endroit où la magie opère! Toute page passée en argument à un layout s'affiche là. Pour en revenir à `HomePage` et `AboutPage`, en les entourant simplement au sein du `<BlogLayout>`, nos deux pages ne font désormais que ce qu'elles sont supposées faire: afficher leur contenu. Nous pouvons maintenant supprimer les imports de `Link`et `Route` puisqu'ils figurent également dans le Layout.

```javascript{3,6}
// web/src/pages/HomePage/HomePage.js

import BlogLayout from 'src/layouts/BlogLayout'

const HomePage = () => {
  return <BlogLayout>Home</BlogLayout>
}

export default HomePage
```

```javascript{4,8-14}
// web/src/pages/AboutPage/AboutPage.js

import { Link, routes } from '@redwoodjs/router'
import BlogLayout from 'src/layouts/BlogLayout'

const AboutPage = () => {
  return (
    <BlogLayout>
        <p>
          Ce site est créé avec pour seule intention de démontrer la puissance créative de Redwood! Oui, c'est très 
          impressionant :D
        </p>
      <Link to={routes.home()}>Return home</Link>
    </BlogLayout>
  )
}

export default AboutPage
```

> **L'alias `src`**
>
> Remarquez que l'import utilise `src/layouts/BlogLayout` et non `../src/layouts/BlogLayout` ou `./src/layouts/BlogLayout`. Pouvoir se contenter d'ajouter uniquement `src` est un petit apport bien pratique de Redwood: `src` est un alias pour le chemin du répertoire `src` du workspace courant. En d'autres termes, lorsque vous travaillez dans `web`, `src` pointe vers `web/src`. Et lorsque vous travaillez dans `api` il pointe vers `api/src`. 

Revenez donc dans votre navigateur, et vous devriez alors voir...... rien de nouveau. Et c'est très bien! Votre layout fonctionne parfaitement.

> **Pourquoi certaines choses sont nommées d'une certaine façon?**
>
> Il est possible que vous ayez remarqué quelques répetitions dans le nom des fichiers utilisés par Redwood. Ainsi les pages se trouvent dans un répertoire appelé `/pages`, et contiennent de nouveau `Page` dans leur nom. Idem pour les Layouts. Pourquoi de choix?
>
> Lorsque vous avez des dizaines de fichiers ouverts dans votre éditeur de code, il est facile de se perdre. C'est d'autant plus le cas lorsque vous avez des fichiers aux noms similaires dans des répertoires différents. A l'usage, il nous est apparut que cette petite répetition dans les noms était au final bien pratique lorsqu'il s'agit de repérer un fichier précis parmi tous les onglets ouverts..
>
> Le plugin [React Developer Tools](https://chrome.google.com/webstore/detail/react-developer-tools/fmkadmapgofadopljbjfkapdkoienihi?hl=en) peut également vous aider à distinguer les fichiers entre eux.
>
> <img src="https://user-images.githubusercontent.com/300/73025189-f970a100-3de3-11ea-9285-15c1116eb59a.png" width="400">

### Retour à la Maison, encore une fois

Ajoutons encore un autre `<Link>` de façon à ce que le titre et le logo pointent vers la page d'accueil:

```javascript{9-11}
// web/src/layouts/BlogLayout/BlogLayout.js

import { Link, routes } from '@redwoodjs/router'

const BlogLayout = ({ children }) => {
  return (
    <>
      <header>
        <h1>
          <Link to={routes.home()}>Redwood Blog</Link>
        </h1>
        <nav>
          <ul>
            <li>
              <Link to={routes.about()}>About</Link>
            </li>
          </ul>
        </nav>
      </header>
      <main>{children}</main>
    </>
  )
}

export default BlogLayout
```

Enfin nous pouvons éliminer de la page About le lien "Retour à la page d'accueil" devenu superflu (ainsi que les imports `Link` et `routes` associés).

```javascript
// web/src/pages/AboutPage/AboutPage.js

import BlogLayout from 'src/layouts/BlogLayout'

const AboutPage = () => {
  return (
    <BlogLayout>
      <p>
        Ce site est créé avec pour seule intention de démontrer la puissance créative de Redwood! Oui, c'est très 
        impressionant :D
      </p>
    </BlogLayout>
  )
}

export default AboutPage
```

## Devenir Dynamique

La seconde partie du didacticiel est disponible en video ici:

<div class="relative pb-9/16">
  <iframe class="absolute inset-0 w-full h-full" src="https://www.youtube.com/embed/SP5vbsWf5Yg?rel=0" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture; modestbranding; showinfo=0" allowfullscreen></iframe>
</div>

Ces deux pages sont plutôt sympas, mais un blog sans article c'est tout de même un peu léger! Travaillons sur ce point à présent.

Pour les besoins de ce didacticiel, nous allons récupérer nos articles depuis la base de données. Puisque les bases de données relationelles sont encore aujourd'hui au coeur de beaucoup d'applications complexes (ou moins complexes d'ailleurs), nous avons fait en sorte de réserver un traitement de première classe aux accès SQL. Dans une application Redwood, tout part du schéma. 

### Créer le schéma de la base de données

Nous devons identifier quelles données seront nécessaires pour un article. Plus tard nous ajouterons d'autres éléments, mais pour commencer nous avons besoin de ceci:

- `ìd` l'identifiant unique pour un article (chaque table de notre base de données aura également un identifiant tel que celui-ci)
- `title` le titre de l'article
- `body` le contenu de l'article
- `createdAt` un 'timestamp' correspondant au moment où l'article est enregistré dans la base de données

Nous utilisons [Prisma Client JS](https://github.com/prisma/prisma-client-js) pour parler vac la base de données. Prisma possède aun autre librairie, appellée [Migrate](https://github.com/prisma/migrate), qui nous permet de mettre à jour le schéma de la base de données en capturant chaque changement successif. Chacun de ces changement est appelé _migration_, et cette librairie Migrate en créé un nouveau à chaque modification du schéma.  

Tout d'abord, définissons la structure d'un article de notre blog dans la base de données. Ouvrez `api/prisma/schema.prisma` et ajoutez la définition de la table `Post` (supprimez au passage tous les modèles présents par défaut dans ce fichier). Une fois terminé, le fichier se présente ainsi: 

```plaintext{13-18}
// api/prisma/schema.prisma

datasource DS {
  provider = "sqlite"
  url      = env("DATABASE_URL")
}

generator client {
  provider      = "prisma-client-js"
  binaryTargets = "native"
}

model Post {
  id        Int      @id @default(autoincrement())
  title     String
  body      String
  createdAt DateTime @default(now())
}
```

Cette série d'instructions signifie que nous voulons créer une table `Post` avec les éléments suivants:

- Un champ `id` de type `Int`, nous précisions à Prisma que cette colonne constitue un identifiant `@id` (de façon à pouvoir créer des relations avec d'autres tables) et que la valeur par `@default` correspond à la fonction Prisma `autoincrement()` impliquant que la base de données insèrera une nouvelle valeur automatiquement lorsqu'un enregistrement est créé.
- Un champ `title` de type `String`
- Un champ `body` également de type `String`
- Un champ `createdAt` de type `DateTime` avec une valeur par `@default` égale à `now()` pour chaque nouvel enregistrement (ainsi nous n'avons pas à nous en charger dans l'application, la base de données le fera pour nous)

> **Identifiant de type Integer vs. identifiant de type String**
>
> Pour le didacticiel, nous resterons simple et utiliserons un identifiant de type Integer. Ceci étant, une application plus évoluée pourra utiliser un identifiant de type CUID ou UUID. Tous deux sont pris en charge par Prisma. Dans ce cas, vous utiliseriez un champ de type `String` au lieu de `Int`, et `cuid()` ou `uuid()` au lieu de `autoincrement()`:
>
> `id String @id @default(cuid())`
>
> Notez que l'utilisation d'un identifiant de type Integer permet d'obtenir des url plus simples comme https://redwoodblog.com/posts/123 instead of https://redwoodblog.com/posts/eebb026c-b661-42fe-93bf-f1a373421a13. 
>
> Allez voir la [documentation officielle de Prisma](https://www.prisma.io/docs/reference/tools-and-interfaces/prisma-schema/data-model#defining-an-id-field) pour plus de détails sur les champs identifiants.

### Migrations

Bon, la création du schéma : c'est fait! Maintenant ce que nous vonlons c'est capturer son état pour en faire une _migration_:

    yarn redwood db save create posts

Ce faisant, vous venez de nommer votre première migration "create posts". Redwood ne tient pas compte de ce nom, mais il est recommandé de choisir un nom significatif pour les autres développeurs de votre équipe.

Une fois la commande exécutée, vous pourrez constater la création d'un nouveau sous-répertoire dans `api/prisma/migrations` avec un _timestamp_ et le nom que vous avez donné votre migration. Ce sous-répertoire contient quelques fichiers: une capture du schéma de la base dans `schema.prisma`, ainsi que la suite de directives que Prima utilise pour effectuer les modifications dans `steps.json`).

Nous allons maintenant appliquer cette migration avec cette commande:

    yarn rw db up

> **Raccourçi `redwood` **
>
> Désormais, nous utiliserons dans nos commandes la forme courte `rw` à la place de `redwood`.

L'exécution de cette commande permet à Prisma d'appliquer les changements sur la base de données, en l'espèce la création d'une nouvelle table `Post` avec les champs définis plus haut.

### Créer une Interface d'Édition d'un Article

Nous n'avons pas encore décidé du look de notre site, mais ne serait-il pas extra si nous pouvions commencer à manipuler nos articles de blog, commencer à créer quelques pages rapidement le temps que l'équipe chargée du design rende sa copie? Heureusement pour nous, "Incroyable" est le petit nom de Redwood :)

Générons tout ce sont nous avons besoin pour réaliser un CRUD (Create, Retrieve, Update, Delete) (Créer, Récupérer, Mettre à jour, Supprimer) sur nos articles. Redwood a justement un generateur spécialement fait pour ça :

    yarn rw g scaffold post

Ouvrons la page `http://localhost:8910/posts` et constatons le résultat:

<img src="https://user-images.githubusercontent.com/300/73027952-53c03080-3de9-11ea-8f5b-d62a3676bbef.png" />

Humm.. ça n'est pas beaucoup plus que ce que nous avions obtenu losque nous avions créé notre première page. Que se passe-t-il lorsque nous cliquons sur le bouton "New Post" (Nouvel Article) ?

<img src="https://user-images.githubusercontent.com/300/73028004-72262c00-3de9-11ea-8924-66d1cc1fceb6.png" />

Ah, maintenant on commence à parler sérieusement! Remplissez donc les champs _title_ (titre) et _body_ (contenu), puis cliquez sur "Save" pour enregistrer.

<img src="https://user-images.githubusercontent.com/300/73028757-08a71d00-3deb-11ea-8813-046c8479b439.png" />

Venons-nous bien de créer un nouvel article? Exactement! Essayez-donc d'en créer d'autres.

<img src="https://user-images.githubusercontent.com/300/73028839-312f1700-3deb-11ea-8e83-0012a3cf689d.png" />

Et maintenant, que se passe-t-il lorsqu'on clique sur "Edit" (éditer) pour l'un de ces articles?

<img src="https://user-images.githubusercontent.com/300/73031307-9802ff00-3df0-11ea-9dc1-ea9af8f21890.png" />

D'accord, et en cliquant sur le bouton "Delete" (supprimer)?

<img src="https://user-images.githubusercontent.com/300/73031339-aea95600-3df0-11ea-9d58-475d9ef43988.png" />

Oui c'est bien ça, en une seule commande, Redwood à créé l'ensemble des pages, composants et services nécessaires aux opérations usuelles de manipulation des articles. Pas même besoin d'ouvrir le gestionnaire de base de données. Redwood appelle ceci des _scaffolds_. Pas mal, non?

Voici dans le détail ce qui arrive lorsqu'on execute la commande `yarn rw g scaffold post` : 

- Ajout d'un fichier _SDL_ pour définir quelques requêtes et mutations GraphQL dans `api/src/graphql/posts.sdl.js` 
- Ajout d'un fichier _service_ `api/src/services/posts/posts.js` qui permet au client Javascript Prisma de manipuler la base de données
- Ajout de quelques _pages_ dans `web/src/pages`:  
  - `EditPostPage` pour éditer un article
  - `NewPostPage` pour créer un nouvel article
  - `PostPage` pour montrer les détails d'un article
  - `PostsPage` pour lister tous les articles
- Ajout de _routes_ pour ces nouvelles pages dans `web/src/Routes.js`
- Ajout de trois _cells_ dans `web/src/components`:
  - `EditPostCell` cellule permettant de récupérer un article pour l'éditer
  - `PostCell` cellule permettant de récupérer un article pour l'afficher
  - `PostsCell` cellule permettant de récupérer tous les articles
- Ajout de quatre _composants_ également dans `web/src/components`:
  - `NewPost` affiche le formulaire permettant la création d'un nouvel article
  - `Post` affiche un article en particulier
  - `PostForm` le formulaire utilisé à la fois par les composants de création et d'édition d'un aricle 
  - `Posts` affiche la table avec l'ensemble des articles

> **Générateurs et conventions de nommage**
>
> Vous remarquerez que certains fichiers générés ont un nom au pluriel, et d'autres au singulier. Cette convention est empruntée au framework Ruby on Rails. Lorsque vous avez à traiter d'un multiple de quelque chose (comme par exemple une liste d'articles), on utilisera le pluriel. Dans le cas contraire (par exemple la création d'un nouvel article), on utilisera le singulier. C'est aussi plus naturel lorsque l'on parle: "montre moi une liste d'articles" vs. "je vais créer un nouvel article".
>
> Pour ce qui concerne les générateurs:
>
> - Les fichiers de Services sont toujours au pluriel.
> - Les méthodes dans les Services sont au singulier ou au pluriel selon qu'ils retournent plusieurs articles ou un seul article (`posts` vs. `createPost`).
> - les fichiers SDL sont toujours au pluriel.
> - Les pages générées par une commande de scaffold sont au pluriel ou au singulier selon que la page manipule plusieurs ou un seul article. Notez que lorsque vous utilisez vous-même un commande `page` en dehors d'un scaffold, le nom utilisé sera simplement celui que vous donnerez.
> - Les Layouts utilisent le nom que vous leur donnez
> - Les composants et les cellules sont au pluriel ou au singulier selon le contexte lorsqu'ils sont générés par scaffolding. Dans le cas contraire, ils utilisent simplement le nom que vous leur donnez.
>
> Remarquez également que seul le nom de la table en base de données et au singulier ou au pluriel, et pas le mot complet. Ainsi on a `PostsCell`, et non `PostCells`. 
>
> Vous n'avez pas à suivre cette convention de façon obligatoire lorsque vous créez vos propres composants, pages, etc... Ceci étant nous vous le recommandons chaudement. Au bout du compte, la communauté Ruby on Rails a fini par s'attacher à cette convention, et ce même si au départ de nombreuses personnes s'y étaient opposées. "[Give it five minutes](https://signalvnoise.com/posts/3124-give-it-five-minutes)" comme disent les anglo-saxons.

### Créer la page d'accueil

Nous pouvons commencer à remplacer ces pages les unes après les autres au fur et à mesure que l'équipe chargée du design nous donne des éléments, ou bien nous pouvons simplement les déplacer dnas la partie "administration" de notre site, et commencer à créer nos propres pages. Ceci étant, la partie publique du site ne va certainement pas autoriser les utilisateurs à créer, éditer ou supprimer les articles. Que peuvent donc faire les utilisateurs?

1. Voir la liste des articles (sans liens pour éditer ou supprimer)
2. Voir le détail d'un article

Puisque nous voudront probablement conserver un moyen de créer et éditer des articles plus tard, conservons les pages générées par scaffolding et créons-en de nouvelles pour ces deux cas de figure.

Nous avons déjà la `HomePage`, pas besoin de créer celle-ci donc. Nous souhaitons afficher une liste d'articles à l'utilisateur donc nous allons devoir ajouter ça. Nous avons besoin de récupérer le contenu depuis la base de données, et nous ne voulons pas que l'utilisateur soit face à une page blanche le temps du chargement (conditions réseau dégradées, serveur géographiquement distant, etc...), donc nous voudrons montrer une sorte de message de chargement et/ou une animation. D'autre part, si une erreur se produit, nous devrons faire en sorte de la prendre en charge. Enfin, nous devrons également prendre en compte le cas où le blog ne contient encore aucun article. 

Wow... notre première page et il semble que nous ayons déjà à nous inquiéter de tant de choses... mais est-ce véritablement le cas ? 

## Cells

These features are common in most web apps. We wanted to see if there was something we could do to make developers' lives easier when it comes to adding them to a typical component. We think we've come up with something to help. We call them _Cells_. Cells provide a simpler and more declarative approach to data fetching. (You can read the full documentation about Cells [here](https://redwoodjs.com/docs/cells).)

When you create a cell you export several specially named constants and then Redwood takes it from there. A typical cell may look something like:

```javascript
export const QUERY = gql`
  query {
    posts {
      id
      title
      body
      createdAt
    }
  }
`

export const Loading = () => <div>Loading...</div>

export const Empty = () => <div>No posts yet!</div>

export const Failure = ({ error }) => (
  <div>Error loading posts: {error.message}</div>
)

export const Success = ({ posts }) => {
  return posts.map((post) => (
    <article>
      <h2>{post.title}</h2>
      <div>{post.body}</div>
    </article>
  ))
}
```

When React renders this component Redwood will:

- Perform the `QUERY` and display the `Loading` component until a response is received
- Once the query returns it will display one of three states:
  - If there was an error, the `Failure` component
  - If the data return is empty (`null` or empty array), the `Empty` component
  - Otherwise, the `Success` component

There are also some lifecycle helpers like `beforeQuery` (for massaging any props before being given to the `QUERY`) and `afterQuery` (for massaging the data returned from GraphQL but before being sent to the `Success` component)

The minimum you need for a cell are the `QUERY` and `Success` exports. If you don't export an `Empty` component, empty results will be sent to your `Success` component. If you don't provide a `Failure` component you'll get error output sent to the console.

A guideline for when to use cells is if your component needs some data from the database or other service that may be delayed in responding. Let Redwood worry about juggling what is displayed when and you can focus on the happy path of the final, rendered component populated with data.

### Our First Cell

The homepage displaying a list of posts is a perfect candidate for our first cell. Naturally, there is a Redwood generator for them:

    yarn rw g cell BlogPosts

This command will result in a new file at `/web/src/components/BlogPostsCell/BlogPostsCell.js` (and a test file) with some boilerplate to get you started:

```javascript
// web/src/components/BlogPostsCell/BlogPostsCell.js

export const QUERY = gql`
  query BlogPostsQuery {
    blogPosts {
      id
    }
  }
`

export const Loading = () => <div>Loading...</div>

export const Empty = () => <div>Empty</div>

export const Failure = ({ error }) => <div>Error: {error.message}</div>

export const Success = ({ blogPosts }) => {
  return JSON.stringify(blogPosts)
}
```

> When generating you can use any case you'd like and Redwood will do the right thing when it comes to naming. These will all create the same filename:
>
>     yarn rw g cell blog_posts
>     yarn rw g cell blog-posts
>     yarn rw g cell blogPosts
>     yarn rw g cell BlogPosts
>
> You will need _some_ kind of indication that you're using more than one word. Calling `yarn redwood g cell blogposts` will generate a file at `web/src/components/BlogpostsCell/BlogpostsCell.js`

To get you off and running as quickly as possible the generator assumes you've got a root GraphQL query named the same thing as your cell and gives you the minimum query needed to get something out of the database. In this case it called the query `blogPosts` which is not a valid query name for our existing Posts SDL and Service. We'll have to rename that to just `posts` in both the query name and prop named in `Success`:

```javascript{5,17,18}
// web/src/components/BlogPostsCell/BlogPostsCell.js

export const QUERY = gql`
  query BlogPostsQuery {
    posts {
      id
    }
  }
`

export const Loading = () => <div>Loading...</div>

export const Empty = () => <div>Empty</div>

export const Failure = ({ error }) => <div>Error: {error.message}</div>

export const Success = ({ posts }) => {
  return JSON.stringify(posts)
}
```

Let's plug this cell into our `HomePage` and see what happens:

```javascript{4,9}
// web/src/pages/HomePage/HomePage.js

import BlogLayout from 'src/layouts/BlogLayout'
import BlogPostsCell from 'src/components/BlogPostsCell'

const HomePage = () => {
  return (
    <BlogLayout>
      <BlogPostsCell />
    </BlogLayout>
  )
}

export default HomePage
```

The browser should actually show an array with a number or two (assuming you created a blog post with our [scaffolding](/tutorial/getting-dynamic#creating-a-post-editor) from earlier). Neat!

<img src="https://user-images.githubusercontent.com/300/73210519-5380a780-40ff-11ea-8639-968507a79b1f.png" />

> **In the `Success` component, where did `posts` come from?**
>
> Notice in the `QUERY` that the query we're making is `posts`. Whatever the name of this query is, that's the name of the prop that will be available in `Success` with your data. You can alias the name of the variable containing the result of the GraphQL query, and that will be the name of the prop:
>
> ```javascript
> export const QUERY = gql`
>   query BlogPostsQuery {
>     postIds: posts {
>       id
>     }
>   }
> `
> ```
>
> Now `postIds` will be available in `Success` instead of `posts`

In addition to the `id` that was added to the `query` by the generator, let's get the title, body, and createdAt too:

```javascript{7-9}
// web/src/components/BlogPostsCell/BlogPostsCell.js

export const QUERY = gql`
  query BlogPostsQuery {
    posts {
      id
      title
      body
      createdAt
    }
  }
`
```

The page should now show a dump of all the data you created for any blog posts you scaffolded:

<img src="https://user-images.githubusercontent.com/300/73210715-abb7a980-40ff-11ea-82d6-61e6bdcd5739.png" />

Now we're in the realm of good ol' React components, so just build out the `Success` component to display the blog post in a nicer format:

```javascript{4-12}
// web/src/components/BlogPostsCell/BlogPostsCell.js

export const Success = ({ posts }) => {
  return posts.map((post) => (
    <article key={post.id}>
      <header>
        <h2>{post.title}</h2>
      </header>
      <p>{post.body}</p>
      <div>Posted at: {post.createdAt}</div>
    </article>
  ))
}
```

And just like that we have a blog! It may be the most basic, ugly blog that ever graced the internet, but it's something! (Don't worry, we've got more features to add.)

<img src="https://user-images.githubusercontent.com/300/73210997-3dbfb200-4100-11ea-847a-602cbf59cb2a.png" />

### Summary

To sum up, what did we actually do to get this far?

1. Generate the homepage
2. Generate the blog layout
3. Define the database schema
4. Run migrations to update the database and create a table
5. Scaffold a CRUD interface to the database table
6. Create a cell to load the data and take care of loading/empty/failure/success states
7. Add the cell to the page

This will become a standard lifecycle of new features as you build a Redwood app.

So far, other than a little HTML, we haven't had to do much by hand. And we especially didn't have to write a bunch of plumbing just to move data from one place to another. It makes web development a little more enjoyable, don't you think?

## Side Quest: How Redwood Works with Data

Redwood likes GraphQL. We think it's the API of the future. Our GraphQL implementation is built with [Apollo](https://www.apollographql.com/). Here's how a typical GraphQL query works its way through your app:

![Redwood Data Flow](https://user-images.githubusercontent.com/300/75402679-50bdd180-58ba-11ea-92c9-bb5a5f4da659.png)

The front-end uses [Apollo Client](https://www.apollographql.com/docs/react/) to create a GraphQL payload sent to [Apollo Server](https://www.apollographql.com/docs/apollo-server/) running in a serverless AWS Lambda function in the cloud.

The `*.sdl.js` files in `api/src/graphql` define the GraphQL [Object](https://www.apollographql.com/docs/tutorial/schema/#object-types), [Query](https://www.apollographql.com/docs/tutorial/schema/#the-query-type) and [Mutation](https://www.apollographql.com/docs/tutorial/schema/#the-mutation-type) types and thus the interface of your API.

Normally you would write a [resolver map](https://www.apollographql.com/docs/tutorial/resolvers/#what-is-a-resolver) that contains all your resolvers and tells Apollo how to map them to your SDL. But putting business logic directly in the resolver map would result in a very big file and horrible reusability, so you'd be well advised to extract all the logic out into a library of functions, import them, and call them from the resolver map, remembering to pass all the arguments through. Ugh, that's a lot of effort and boilerplate, and still doesn't result in very good reusabilty.

Redwood has a better way! Remember the `api/src/services` directory? Redwood will automatically import and map resolvers from the corresponding **services** file onto your SDL. At the same time, it allows you to write those resolvers in a way that makes them easy to call as regular functions from other resolvers or services. That's a lot of awesomeness to contemplate, so let's show an example.

Consider the following SDL javascript snippet:

```javascript
// api/src/graphql/posts.sdl.js

export const schema = gql`
  type Post {
    id: Int!
    title: String!
    body: String!
    createdAt: DateTime!
  }

  type Query {
    posts: [Post!]!
    post(id: Int!): Post!
  }

  input CreatePostInput {
    title: String!
    body: String!
  }

  input UpdatePostInput {
    title: String
    body: String
  }

  type Mutation {
    createPost(input: CreatePostInput!): Post!
    updatePost(id: Int!, input: UpdatePostInput!): Post!
    deletePost(id: Int!): Post!
  }
`
```

In this example, Redwood will look in `api/src/services/posts/posts.js` for the following five resolvers:

- `posts()`
- `post({id})`
- `createPost({input})`
- `updatePost({id, input})`
- `deletePost({id})`

To implement these, simply export them from the services file. They will usually get your data from a database, but they can do anything you want, as long as they return the proper types that Apollo expects based on what you defined in `posts.sdl.js`.

```javascript
// api/src/services/posts/posts.js
import { db } from 'src/lib/db'

export const posts = () => {
  return db.post.findMany()
}

export const post = ({ id }) => {
  return db.post.findOne({
    where: { id },
  })
}

export const createPost = ({ input }) => {
  return db.post.create({
    data: input,
  })
}

export const updatePost = ({ id, input }) => {
  return db.post.update({
    data: input,
    where: { id },
  })
}

export const deletePost = ({ id }) => {
  return db.post.delete({
    where: { id },
  })
}
```

> Apollo assumes these functions return promises, which `db` (an instance of `PrismaClient`) does. Apollo waits for them to resolve before responding with your query results, so you don't need to worry about `async`/`await` or mess with callbacks yourself.

You may be wondering why we call these implementation files "services". While this example blog doesn't get complex enough to show it off, services are intended to be an abstraction **above** single database tables. For example, a more complex app may have a "billing" service that uses both a `transactions` table and a `subscriptions` table. Some of the functionality of this service may be exposed via GraphQL, but only as much as you like.

You don't have to make each function in your service available via GraphQL—leave it out of your `Query` and `Mutation` types and it won't exist as far as GraphQL is concerned. But you could still use it yourself—services are just Javascript functions so you can use them anywhere you'd like:

- From another service
- In a custom lambda function
- From a completely separate, custom API

By dividing your app into well-defined services and providing an API for those services (both for internal use **and** for GraphQL), you will naturally start to enforce separation of concerns and (in all likelihood) increase the maintainability of your codebase.

Back to our data flow: Apollo has called the resolver which, in our case, retrieved data from the database. Apollo digs into the object and returns only the key/values that were asked for in the GraphQL query. It then packages up the response in a GraphQL payload and returns it to the browser.

If you're using a Redwood **cell** then this data will be available to you in your `Success` component ready to be looped through and/or displayed like any other React component.

## Routing Params

Now that we have our homepage listing all the posts, let's build the "detail" page—a canonical URL that displays a single post. First we'll generate the page and route:

    yarn rw g page BlogPost

> Note that we can't call this page simply `Post` because our scaffold already created a page with that name.

Now let's link the title of the post on the homepage to the detail page (and include the `import` for `Link` and `routes`):

```javascript{3,12}
// web/src/components/BlogPostsCell/BlogPostsCell.js

import { Link, routes } from '@redwoodjs/router'

// QUERY, Loading, Empty and Failure definitions...

export const Success = ({ posts }) => {
  return posts.map((post) => (
    <article key={post.id}>
      <header>
        <h2>
          <Link to={routes.blogPost()}>{post.title}</Link>
        </h2>
      </header>
      <p>{post.body}</p>
      <div>Posted at: {post.createdAt}</div>
    </article>
  ))
}
```

If you click the link on the title of the blog post you should see the boilerplate text on `BlogPostPage`. But what we really need is to specify _which_ post we want to view on this page. It would be nice to be able to specify the ID of the post in the URL with something like `/blog-post/1`. Let's tell the `<Route>` to expect another part of the URL, and when it does, give that part a name that we can reference later:

```html
// web/src/Routes.js

<Route path="/blog-post/{id}" page={BlogPostPage} name="blogPost" />
```

Notice the `{id}`. Redwood calls these _route parameters_. They say "whatever value is in this position in the path, let me reference it by the name inside the curly braces."

Cool, cool, cool. Now we need to construct a link that has the ID of a post in it:

```html
// web/src/components/BlogPostsCell/BlogPostsCell.js

<Link to={routes.blogPost({ id: post.id })}>{post.title}</Link>
```

For routes with route parameters, the named route function expects an object where you specify a value for each parameter. If you click on the link now, it will indeed take you to `/blog-post/1` (or `/blog-post/2`, etc, depending on the ID of the post).

### Using the Param

Ok, so the ID is in the URL. What do we need next in order to display a specific post? It sounds like we'll be doing some data retrieval from the database, which means we want a cell:

    yarn rw g cell BlogPost

And then we'll use that cell in `BlogPostPage` (and while we're at it let's surround the page with the `BlogLayout`):

```javascript
// web/src/pages/BlogPostPage/BlogPostPage.js

import BlogLayout from 'src/layouts/BlogLayout'
import BlogPostCell from 'src/components/BlogPostCell'

const BlogPostPage = () => {
  return (
    <BlogLayout>
      <BlogPostCell />
    </BlogLayout>
  )
}

export default BlogPostPage
```

Now over to the cell, we need access to that `{id}` route param so we can look up the ID of the post in the database. Let's update the query to accept a variable (and again change the query name from `blogPost` to just `post`)

```javascript{4,5,7-9,20,21}
// web/src/components/BlogPostCell/BlogPostCell.js

export const QUERY = gql`
  query BlogPostQuery($id: Int!) {
    post(id: $id) {
      id
      title
      body
      createdAt
    }
  }
`

export const Loading = () => <div>Loading...</div>

export const Empty = () => <div>Empty</div>

export const Failure = ({ error }) => <div>Error: {error.message}</div>

export const Success = ({ post }) => {
  return JSON.stringify(post)
}
```

Okay, we're getting closer. Still, where will that `$id` come from? Redwood has another trick up its sleeve. Whenever you put a route param in a route, that param is automatically made available to the page that route renders. Which means we can update `BlogPostPage` to look like this:

```javascript{3,6}
// web/src/pages/BlogPostPage/BlogPostPage.js

const BlogPostPage = ({ id }) => {
  return (
    <BlogLayout>
      <BlogPostCell id={id} />
    </BlogLayout>
  )
}
```

`id` already exists since we named our route param `{id}`. Thanks Redwood! But how does that `id` end up as the `$id` GraphQL parameter? If you've learned anything about Redwood by now, you should know it's going to take care of that for you! By default, any props you give to a cell will automatically be turned into variables and given to the query. "Say what!" you're saying. It's true!

We can prove it! Try going to the detail page for a post in the browser and—uh oh. Hmm:

![image](https://user-images.githubusercontent.com/300/75820346-096b9100-5d51-11ea-8f6e-53fda78d1ed5.png)

> By the way, this error message you're seeing is thanks to the `Failure` section of our Cell!

If you take a look in the web inspector console you can see the actual error coming from GraphQL:

    [GraphQL error]: Message: Variable "$id" got invalid value "1";
      Expected type Int. Int cannot represent non-integer value: "1",
      Location: [object Object], Path: undefined

It turns out that route params are extracted as strings from the URL, but GraphQL wants an integer for the ID. We could use `parseInt()` to convert it to a number before passing it into `BlogPostCell`, but honestly, we can do better than that!

### Route Param Types

What if you could request the conversion right in the route's path? Well, guess what: you can! Introducing **route param types**. It's as easy as adding `:Int` to our existing route param:

```html
// web/src/Routes.js

<Route path="/blog-post/{id:Int}" page={BlogPostPage} name="blogPost" />
```

Voilà! Not only will this convert the `id` param to a number before passing it to your Page, it will prevent the route from matching unless the `id` path segment consists entirely of digits. If any non-digits are found, the router will keep trying other routes, eventually showing the `NotFoundPage` if no routes match.

> **What if I want to pass some other prop to the cell that I don't need in the query, but do need in the Success/Loader/etc. components?**
>
> All of the props you give to the cell will be automatically available as props in the render components. Only the ones that match the GraphQL variables list will be given to the query. You get the best of both worlds! In our post display above, if you wanted to display some random number along with the post (for some contrived, tutorial-like reason), just pass that prop:
>
> ```javascript
> <BlogPostCell id={id} rand={Math.random()} />
> ```
>
> And get it, along with the query result (and even the original `id` if you want) in the component:
>
> ```javascript
> export const Success = ({ post, id, rand }) => {
>   //...
> }
> ```
>
> Thanks again, Redwood!

### Displaying a Blog Post

Now let's display the actual post instead of just dumping the query result. This seems like the perfect place for a good old fashioned component since we're displaying a post on both the home page and this detail page, and it's (currently) the same exact output. Let's Redwood-up a component (I just invented that phrase):

    yarn rw g component BlogPost

Which creates `web/src/components/BlogPost/BlogPost.js` (and test!) as a super simple React component:

```javascript
// web/src/components/BlogPost/BlogPost.js

const BlogPost = () => {
  return (
    <div>
      <h2>{'BlogPost'}</h2>
      <p>{'Find me in ./web/src/components/BlogPost/BlogPost.js'}</p>
    </div>
  )
}

export default BlogPost
```

> You may notice we don't have any explicit `import` statements for `React` itself. We (the Redwood dev team) got tired of constantly importing it over and over again in every file so we automatically import it for you!

Let's take the post display code out of `BlogPostsCell` and put it here instead, taking the `post` in as a prop:

```javascript{3,5,7-14}
// web/src/components/BlogPost/BlogPost.js

import { Link, routes } from '@redwoodjs/router'

const BlogPost = ({ post }) => {
  return (
    <article>
      <header>
        <h2>
          <Link to={routes.blogPost({ id: post.id })}>{post.title}</Link>
        </h2>
      </header>
      <div>{post.body}</div>
    </article>
  )
}

export default BlogPost
```

And update `BlogPostsCell` and `BlogPostCell` to use this new component instead:

```javascript{3,8}
// web/src/components/BlogPostsCell/BlogPostsCell.js

import BlogPost from 'src/components/BlogPost'

// Loading, Empty, Failure...

export const Success = ({ posts }) => {
  return posts.map((post) => <BlogPost key={post.id} post={post} />)
}
```

```javascript{3,8}
// web/src/components/BlogPostCell/BlogPostCell.js

import BlogPost from 'src/components/BlogPost'

// Loading, Empty, Failure...

export const Success = ({ post }) => {
  return <BlogPost post={post} />
}
```

And there we go! We should be able to move back and forth between the homepage and the detail page.

> If you like what you've been seeing from the router, you can dive deeper into the [Redwood Router](/docs/redwood-router) guide.

### Summary

Let's summarize:

1. We created a new page to show a single post (the "detail" page).
2. We added a route to handle the `id` of the post and turn it into a route param.
3. We created a cell to fetch and display the post.
4. Redwood made the world a better place by making that `id` available to us at several key junctions in our code and even turning it into a number automatically.
5. We turned the actual post display into a standard React component and used it in both the homepage and new detail page.

## Everyone's Favorite Thing to Build: Forms

Wait, don't close your browser! You had to know this was coming eventually, didn't you? And you've probably realized by now we wouldn't even have this section in the tutorial unless Redwood had figured out a way to make forms less soul-sucking than usual. In fact Redwood might even make you _love_ building forms. Well, love is a strong word. _Like_ building forms. _Tolerate_ building them?

Part 3 of the video tutorial picks up here:

<div class="relative pb-9/16">
  <iframe class="absolute inset-0 w-full h-full" src="https://www.youtube.com/embed/eT7iIy0F8Tk?rel=0" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture; modestbranding; showinfo=0" allowfullscreen></iframe>
</div>

We already have a form or two in our app; remember our posts scaffold? And those work pretty well! How hard can it be? (Hopefully you haven't sneaked a peek at that code—what's coming next will be much more impressive if you haven't.)

Let's build the simplest form that still makes sense for our blog, a "contact us" form.

### The Page

    yarn rw g page contact

We can put a link to Contact in our layout's header:

```javascript{17-19}
// web/src/layouts/BlogLayout/BlogLayout.js

import { Link, routes } from '@redwoodjs/router'

const BlogLayout = ({ children }) => {
  return (
    <>
      <header>
        <h1>
          <Link to={routes.home()}>Redwood Blog</Link>
        </h1>
        <nav>
          <ul>
            <li>
              <Link to={routes.about()}>About</Link>
            </li>
            <li>
              <Link to={routes.contact()}>Contact</Link>
            </li>
          </ul>
        </nav>
      </header>
      <main>{children}</main>
    </>
  )
}

export default BlogLayout
```

And then use the `BlogLayout` in the `ContactPage`:

```javascript{3,6}
// web/src/pages/ContactPage/ContactPage.js

import BlogLayout from 'src/layouts/BlogLayout'

const ContactPage = () => {
  return <BlogLayout></BlogLayout>
}

export default ContactPage
```

Double check that everything looks good and then let's get to the good stuff.

### Introducing Form Helpers

Forms in React are infamously annoying to work with. There are [Controlled Components](https://reactjs.org/docs/forms.html#controlled-components) and [Uncontrolled Components](https://reactjs.org/docs/uncontrolled-components.html) and [third party libraries](https://jaredpalmer.com/formik/) and many more workarounds to try and make forms in React as simple as they were originally intended to be in the HTML spec: an `<input>` field with a `name` attribute that gets submitted somewhere when you click a button.

We think Redwood is a step or two in the right direction by not only freeing you from writing controlled component plumbing, but also dealing with validation and errors automatically. Let's see how it works.

Before we start, let's add a couple of CSS classes to make the default form layout a little cleaner and save us from having to write a bunch of `style` attribute that will clutter up the examples and make them harder to follow. For now we'll just put these in the root `index.css` file in `web/src`:

```css
/* web/src/index.css */

button, input, label, textarea {
  display: block;
  outline: none;
}

label {
  margin-top: 1rem;
}

.error {
  color: red;
}

input.error, textarea.error {
  border: 1px solid red;
}
```

For now we won't be talking to the database in our Contact form so we won't create a cell. Let's create the form right on the page. Redwood forms start with the...wait for it...`<Form>` tag:

```javascript{3,9}
// web/src/pages/ContactPage/ContactPage.js

import { Form } from '@redwoodjs/forms'
import BlogLayout from 'src/layouts/BlogLayout'

const ContactPage = () => {
  return (
    <BlogLayout>
      <Form></Form>
    </BlogLayout>
  )
}

export default ContactPage
```

Well that was anticlimactic. You can't even see it in the browser. Let's add a form field so we can at least see something. Redwood ships with several inputs and a plain text input box is `<TextField>`. We'll also give the field a `name` attribute so that once there are multiple inputs on this page we'll know which contains which data:

```javascript{3,10}
// web/src/pages/ContactPage/ContactPage.js

import { Form, TextField } from '@redwoodjs/forms'
import BlogLayout from 'src/layouts/BlogLayout'

const ContactPage = () => {
  return (
    <BlogLayout>
      <Form>
        <TextField name="input" />
      </Form>
    </BlogLayout>
  )
}

export default ContactPage
```

<img src="https://user-images.githubusercontent.com/300/80258121-4f4d2300-8637-11ea-83f5-c667e05aaf74.png" />

Something is showing! Still, pretty boring. How about adding a submit button?

```javascript{3,11}
// web/src/pages/ContactPage/ContactPage.js

import { Form, TextField, Submit } from '@redwoodjs/forms'
import BlogLayout from 'src/layouts/BlogLayout'

const ContactPage = () => {
  return (
    <BlogLayout>
      <Form>
        <TextField name="input" />
        <Submit>Save</Submit>
      </Form>
    </BlogLayout>
  )
}

export default ContactPage
```

<img src="https://user-images.githubusercontent.com/300/80258188-7572c300-8637-11ea-9583-1b7636f93be0.png" />

We have what might actually be considered a real, bonafide form here. Try typing something in and clicking "Save". Nothing blew up on the page but we have no indication that the form submitted or what happened to the data (although you may have noticed an error in the Web Inspector). Next we'll get the data in our fields.

### onSubmit

Similar to a plain HTML form we'll give `<Form>` an `onSubmit` handler. That handler will be called with a single argument—an object containing all of the submitted form fields:

```javascript{4-6,10}
// web/src/pages/ContactPage/ContactPage.js

const ContactPage = () => {
  const onSubmit = (data) => {
    console.log(data)
  }

  return (
    <BlogLayout>
      <Form onSubmit={onSubmit}>
        <TextField name="input" />
        <Submit>Save</Submit>
      </Form>
    </BlogLayout>
  )
}
```

Now try filling in some data and submitting:

<img src="https://user-images.githubusercontent.com/300/80258293-c08cd600-8637-11ea-92fb-93d3ca1db3cf.png" />

Great! Let's turn this into a more useful form by adding a couple fields. We'll rename the existing one to "name" and add "email" and "message":

```javascript{3,15,16}
// web/src/pages/ContactPage/ContactPage.js

import { Form, TextField, TextAreaField, Submit } from '@redwoodjs/forms'
import BlogLayout from 'src/layouts/BlogLayout'

const ContactPage = () => {
  const onSubmit = (data) => {
    console.log(data)
  }

  return (
    <BlogLayout>
      <Form onSubmit={onSubmit}>
        <TextField name="name" />
        <TextField name="email" />
        <TextAreaField name="message" />
        <Submit>Save</Submit>
      </Form>
    </BlogLayout>
  )
}

export default ContactPage
```

See the new `<TextAreaField>` component here which generates an HTML `<textarea>` but that contains Redwood's form goodness:

<img src="https://user-images.githubusercontent.com/300/80258346-e4e8b280-8637-11ea-908b-06a1160b932b.png" />

Let's add some labels:

```javascript{6,9,12}
// web/src/pages/ContactPage/ContactPage.js

return (
  <BlogLayout>
    <Form onSubmit={onSubmit}>
      <label htmlFor="name">Name</label>
      <TextField name="name" />

      <label htmlFor="email">Email</label>
      <TextField name="email" />

      <label htmlFor="message">Message</label>
      <TextAreaField name="message" />

      <Submit>Save</Submit>
    </Form>
  </BlogLayout>
)
```

<img src="https://user-images.githubusercontent.com/300/80258431-15c8e780-8638-11ea-8eca-0bd222b51d8a.png" />

Try filling out the form and submitting and you should get a console message with all three fields now.

### Validation

"Okay Redwood tutorial author," you're saying, "what's the big deal? You built up Redwood's form helpers as The Next Big Thing but there are plenty of libraries that will let me skip creating controlled inputs manually. So what?" And you're right! Anyone can fill out a form _correctly_ (although there are plenty of QA folks who would challenge that statement), but what happens when someone leaves something out, or makes a mistake, or tries to haxorz our form? Now who's going to be there to help? Redwood, that's who!

All three of these fields should be required in order for someone to send a message to us. Let's enforce that with the standard HTML `required` attribute:

```javascript{7,10,13}
// web/src/pages/ContactPage/ContactPage.js

return (
  <BlogLayout>
    <Form onSubmit={onSubmit}>
      <label htmlFor="name">Name</label>
      <TextField name="name" required />

      <label htmlFor="email">Email</label>
      <TextField name="email" required />

      <label htmlFor="message">Message</label>
      <TextAreaField name="message" required />

      <Submit>Save</Submit>
    </Form>
  </BlogLayout>
)
```

<img src="https://user-images.githubusercontent.com/300/80258542-5163b180-8638-11ea-8450-8a727de177ad.png" />

Now when trying to submit there'll be message from the browser noting that a field must be filled in. This is better than nothing, but these messages can't be styled. Can we do better?

Yes! Let's update that `required` call to instead be an object we pass to a custom attribute on Redwood form helpers called `validation`:

```javascript{7,10,13}
// web/src/pages/ContactPage/ContactPage.js

return (
  <BlogLayout>
    <Form onSubmit={onSubmit}>
      <label htmlFor="name">Name</label>
      <TextField name="name" validation={{ required: true }} />

      <label htmlFor="email">Email</label>
      <TextField name="email" validation={{ required: true }} />

      <label htmlFor="message">Message</label>
      <TextAreaField name="message" validation={{ required: true }} />

      <Submit>Save</Submit>
    </Form>
  </BlogLayout>
)
```

And now when we submit the form with blank fields...the Name field gets focus. Boring. But this is just a stepping stone to our amazing reveal! We have one more form helper component to add—the one that displays errors on a field. Oh it just so happens that it's plain HTML so we can style it however we want!

### `<FieldError>`

Introducing `<FieldError>` (don't forget to include it in the `import` statement at the top):

```javascript{8,22,26,30}
// web/src/pages/ContactPage/ContactPage.js

import {
  Form,
  TextField,
  TextAreaField,
  Submit,
  FieldError,
} from '@redwoodjs/forms'
import BlogLayout from 'src/layouts/BlogLayout'

const ContactPage = () => {
  const onSubmit = (data) => {
    console.log(data)
  }

  return (
    <BlogLayout>
      <Form onSubmit={onSubmit}>
        <label htmlFor="name">Name</label>
        <TextField name="name" validation={{ required: true }} />
        <FieldError name="name" />

        <label htmlFor="email">Email</label>
        <TextField name="email" validation={{ required: true }} />
        <FieldError name="email" />

        <label htmlFor="message">Message</label>
        <TextAreaField name="message" validation={{ required: true }} />
        <FieldError name="message" />

        <Submit>Save</Submit>
      </Form>
    </BlogLayout>
  )
}

export default ContactPage
```

Note that the `name` attribute matches the `name` of the input field above it. That's so it knows which field to display errors for. Try submitting that form now.

<img src="https://user-images.githubusercontent.com/300/80258694-ac95a400-8638-11ea-904c-dc034f07b12a.png" />

But this is just the beginning. Let's make sure folks realize this is an error message. Remember the `.error` class we defined in `index.css`? Check out the `className` attribute on `<FieldError>`:

```javascript{8,12,16}
// web/src/pages/ContactPage/ContactPage.js

return (
  <BlogLayout>
    <Form onSubmit={onSubmit}>
      <label htmlFor="name">Name</label>
      <TextField name="name" validation={{ required: true }} />
      <FieldError name="name" className="error" />

      <label htmlFor="email">Email</label>
      <TextField name="email" validation={{ required: true }} />
      <FieldError name="email" className="error" />

      <label htmlFor="message">Message</label>
      <TextAreaField name="message" validation={{ required: true }} />
      <FieldError name="message" className="error" />

      <Submit>Save</Submit>
    </Form>
  </BlogLayout>
)
```

<img src="https://user-images.githubusercontent.com/300/73306040-3cf65100-41d0-11ea-99a9-9468bba82da7.png" />

You know what would be nice, if the input itself somehow displayed the fact that there was an error. Check out the `errorClassName` attributes on the inputs:

```javascript{10,18,26}
// web/src/pages/ContactPage/ContactPage.js

return (
  <BlogLayout>
    <Form onSubmit={onSubmit}>
      <label htmlFor="name">Name</label>
      <TextField
        name="name"
        validation={{ required: true }}
        errorClassName="error"
      />
      <FieldError name="name" className="error" />

      <label htmlFor="email">Email</label>
      <TextField
        name="email"
        validation={{ required: true }}
        errorClassName="error"
      />
      <FieldError name="email" className="error" />

      <label htmlFor="message">Message</label>
      <TextAreaField
        name="message"
        validation={{ required: true }}
        errorClassName="error"
      />
      <FieldError name="message" className="error" />

      <Submit>Save</Submit>
    </Form>
  </BlogLayout>
)
```

<img src="https://user-images.githubusercontent.com/300/80258907-39d8f880-8639-11ea-8816-03a11c69e8ac.png" />

Oooo, what if the _label_ could change as well? It can, but we'll need Redwood's custom `<Label>` component for that (note that `for` becomes `name` just like the other components). Don't forget the import:

```javascript{9,21-23,31-33,41-43}
// web/src/pages/ContactPage/ContactPage.js

import {
  Form,
  TextField,
  TextAreaField,
  Submit,
  FieldError,
  Label,
} from '@redwoodjs/forms'
import BlogLayout from 'src/layouts/BlogLayout'

const ContactPage = () => {
  const onSubmit = (data) => {
    console.log(data)
  }

  return (
    <BlogLayout>
      <Form onSubmit={onSubmit}>
        <Label name="name" errorClassName="error">
          Name
        </Label>
        <TextField
          name="name"
          validation={{ required: true }}
          errorClassName="error"
        />
        <FieldError name="name" className="error" />

        <Label name="email" errorClassName="error">
          Email
        </Label>
        <TextField
          name="email"
          validation={{ required: true }}
          errorClassName="error"
        />
        <FieldError name="email" className="error" />

        <Label name="message" errorClassName="error">
          Message
        </Label>
        <TextAreaField
          name="message"
          validation={{ required: true }}
          errorClassName="error"
        />
        <FieldError name="message" className="error" />

        <Submit>Save</Submit>
      </Form>
    </BlogLayout>
  )
}

export default ContactPage
```

<img src="https://user-images.githubusercontent.com/300/80259003-70af0e80-8639-11ea-97cf-b6b816118fbf.png" />

> In addition to `className` and `errorClassName` you can also use `style` and `errorStyle`

### Validating Input Format

We should make sure the email field actually contains an email:

```html{7-9}
// web/src/pages/ContactPage/ContactPage.js

<TextField
  name="email"
  validation={{
    required: true,
    pattern: {
      value: /[^@]+@[^.]+\..+/,
    },
  }}
  errorClassName="error"
/>
```

That is definitely not the end-all-be-all for email address validation, but pretend it's bulletproof. Let's also change the message on the email validation to be a little more friendly:

```html{9}
// web/src/pages/ContactPage/ContactPage.js

<TextField
  name="email"
  validation={{
    required: true,
    pattern: {
      value: /[^@]+@[^.]+\..+/,
      message: 'Please enter a valid email address',
    },
  }}
  errorClassName="error"
/>
```

<img src="https://user-images.githubusercontent.com/300/80259139-bd92e500-8639-11ea-99d5-be278dc67afc.png" />

You may have noticed that trying to submit a form with validation errors outputs nothing to the console—it's not actually submitting. That's a good thing! Fix the errors and all is well.

> When a validation error appears it will _disappear_ as soon as you fix the content of the field. You don't have to click "Submit" again to remove the error messages.

Finally, you know what would _really_ be nice: if the fields were validated as soon as the user leaves each one so they don't fill out the whole thing and submit just to see multiple errors appear. Let's do that:

```html
// web/src/pages/ContactPage/ContactPage.js

<Form onSubmit={onSubmit} validation={{ mode: 'onBlur' }}>
```

Well, what do you think? Was it worth the hype? A couple of new components and you've got forms that handle validation and wrap up submitted values in a nice data object, all for free.

> Redwood's forms are built on top of [React Hook Form](https://react-hook-form.com/) so there is even more functionality available than we've documented here.

Redwood has one more trick up its sleeve when it comes to forms but we'll save that for when we're actually submitting one to the server.

Having a contact form is great, but only if you actually get the contact somehow. Let's create a database table to hold the submitted data and create our first GraphQL mutation.

## Saving Data

Let's add a new database table. Open up `api/prisma/schema.prisma` and add a Contact model after the Post model that's there now:

```javascript
// api/prisma/schema.prisma

model Contact {
  id        Int @id @default(autoincrement())
  name      String
  email     String
  message   String
  createdAt DateTime @default(now())
}
```

> To mark a column as optional (that is, allowing `NULL` as a value) you can suffix the datatype with question mark: `name String?`

Next we create a migration file:

    yarn rw db save create contact

Finally we execute the migration to run the DDL commands to upgrade the database:

    yarn rw db up

Now we'll create the GraphQL interface to access this table. We haven't used this `generate` command yet (although the `scaffold` command did use it behind the scenes):

    yarn rw g sdl contact

Just like the `scaffold` command, this will create two new files under the `api` directory:

1. `api/src/graphql/contacts.sdl.js`: defines the GraphQL schema in GraphQL's schema definition language
2. `api/src/services/contacts/contacts.js`: contains your app's business logic.

Open up `api/src/graphql/contacts.sdl.js` and you'll see the `Contact`, `CreateContactInput` and `UpdateContactInput` types were already defined for us—the `generate sdl` command introspected the schema and created a `Contact` type containing each database field in the table, as well as a `Query` type with a single query `contacts` which returns an array of `Contact` types:

```javascript
// api/src/graphql/contacts.sdl.js

export const schema = gql`
  type Contact {
    id: Int!
    name: String!
    email: String!
    message: String!
    createdAt: DateTime!
  }

  type Query {
    contacts: [Contact!]!
  }

  input CreateContactInput {
    name: String!
    email: String!
    message: String!
  }

  input UpdateContactInput {
    name: String
    email: String
    message: String
  }
`
```

What's `CreateContactInput` and `UpdateContactInput`? Redwood follows the GraphQL recommendation of using [Input Types](https://graphql.org/graphql-js/mutations-and-input-types/) in mutations rather than listing out each and every field that can be set. Any fields required in `schema.prisma` are also required in `CreateContactInput` (you can't create a valid record without them) but nothing is explictly required in `UpdateContactInput`. This is because you could want to update only a single field, or two fields, or all fields. The alternative would be to create separate Input types for every permutation of fields you would want to update. We felt that only having one update input, while maybe not pedantically the absolute **correct** way to create a GraphQL API, was a good compromise for optimal developer experience.

> Redwood assumes your code won't try to set a value on any field named `id` or `createdAt` so it left those out of the Input types, but if your database allowed either of those to be set manually you can update `CreateContactInput` or `UpdateContactInput` and add them.

Since all of the DB columns were required in the `schema.prisma` file they are marked as required here (the `!` suffix on the datatype).

> **Remember:** `schema.prisma` syntax requires an extra `?` character when a field is _not_ required, GraphQL's SDL syntax requires an extra `!` when a field _is_ required.

As described in [Side Quest: How Redwood Deals with Data](side-quest-how-redwood-works-with-data) there are no explicit resolvers defined in the SDL file. Redwood follows a simple naming convention—each field listed in the `Query` and `Mutation` types map to a function with the same name in the `services` file and in the `sdl` file (`api/src/graphql/contacts.sdl.js -> api/src/services/contacts/contacts.js`)

In this case we're creating a single `Mutation` that we'll call `createContact`. Add that to the end of the SDL file (before the closing backtick):

```javascript
// api/src/graphql/contacts.sdl.js

type Mutation {
  createContact(input: CreateContactInput!): Contact
}
```

The `createContact` mutation will accept a single variable, `input`, that is an object that conforms to what we expect for a `CreateContactInput`, namely `{ name, email, message }`.

That's it for the SDL file, let's define the service that will actually save the data to the database. The service includes a default `contacts` function for getting all contacts from the database. Let's add our mutation to create a new contact:

```javascript{9-11}
// api/src/services/contacts/contacts.js

import { db } from 'src/lib/db'

export const contacts = () => {
  return db.contact.findMany()
}

export const createContact = ({ input }) => {
  return db.contact.create({ data: input })
}
```

Thanks to Prisma Client JS it takes very little code to actually save something to the database! This is an asynchronous call but we didn't have to worry about resolving Promises or dealing with `async/await`. Apollo will do that for us!

Before we plug this into the UI, let's take a look at a nifty GUI you get just by running `yarn redwood dev`.

### GraphQL Playground

Often it's nice to experiment and call your API in a more "raw" form before you get too far down the path of implementation only to find out something is missing. Is there a typo in the API layer or the web layer? Let's find out by accessing just the API layer.

When you started development with `yarn redwood dev` you actually started a second process running at the same time. Open a new browser tab and head to http://localhost:8911/graphql This is Prisma's [GraphQL Playground](https://github.com/prisma-labs/graphql-playground), a web-based GUI for GraphQL APIs:

<img src="https://user-images.githubusercontent.com/300/70950852-9b97af00-2016-11ea-9550-b6983ce664e2.png" />

Not very exciting yet, but check out that "Docs" tab on the far right:

<img src="https://user-images.githubusercontent.com/300/73311311-fce89b80-41da-11ea-9a7f-2ef6b8191052.png" />

It's the complete schema as defined by our SDL files! The Playground will ingest these definitions and give you autocomplete hints on the left to help you build queries from scratch. Try getting the IDs of all the posts in the database; type the query at the left and then click the "Play" button to execute:

<img src="https://user-images.githubusercontent.com/300/70951466-52e0f580-2018-11ea-91d6-5a5712858781.png" />

The GraphQL Playground is a great way to experiment with your API or troubleshoot when you come across a query or mutation that isn't behaving in the way you expect.

### Creating a Contact

Our GraphQL mutation is ready to go on the backend so all that's left is to invoke it on the frontend. Everything related to our form is in `ContactPage` so that's the logical place to put the mutation call. First we define the mutation as a constant that we call later (this can be defined outside of the component itself, right after the `import` statements):

```javascript
// web/src/pages/ContactPage/ContactPage.js

const CREATE_CONTACT = gql`
  mutation CreateContactMutation($input: CreateContactInput!) {
    createContact(input: $input) {
      id
    }
  }
`
```

We reference the `createContact` mutation we defined in the Contacts SDL passing it an `input` object which will contain the actual name, email and message fields.

Next we'll call the `useMutation` hook provided by Apollo which will allow us to execute the mutation when we're ready (don't forget the `import` statement):

```javascript{11,15}
// web/src/pages/ContactPage/ContactPage.js

import {
  Form,
  TextField,
  TextAreaField,
  Submit,
  FieldError,
  Label,
} from '@redwoodjs/forms'
import { useMutation } from '@redwoodjs/web'
import BlogLayout from 'src/layouts/BlogLayout'

const ContactPage = () => {
  const [create] = useMutation(CREATE_CONTACT)

  const onSubmit = (data) => {
    console.log(data)
  }

  return (...)
}
```

`create` is a function that invokes the mutation and takes an object with a `variables` key, containing another object with an `input` key. As an example, we could call it like:

```javascript
create({
  variables: {
    input: {
      name: 'Rob',
      email: 'rob@redwoodjs.com',
      message: 'I love Redwood!',
    },
  },
})
```

If you'll recall `<Form>` gives us all of the fields in a nice object where the key is the name of the field, which means the `data` object we're receiving in `onSubmit` is already in the proper format that we need for the `input`!

Now we can update the `onSubmit` function to invoke the mutation with the data it receives:

```javascript{7}
// web/src/pages/ContactPage/ContactPage.js

const ContactPage = () => {
  const [create] = useMutation(CREATE_CONTACT)

  const onSubmit = (data) => {
    create({ variables: { input: data }})
    console.log(data)
  }

  return (...)
}
```

Try filling out the form and submitting—you should have a new Contact in the database! You can verify that with the GraphQL Playground if you were so inclined:

![image](https://user-images.githubusercontent.com/300/76250632-ed5d6900-6202-11ea-94ce-bd88e3a11ade.png)

### Improving the Contact Form

Our contact form works but it has a couple of issues at the moment:

- Clicking the submit button multiple times will result in multiple submits
- The user has no idea if their submission was successful
- If an error was to occur on the server, we have no way of notifying the user

Let's address these issues.

The `useMutation` hook returns a couple more elements along with the function to invoke it. We can destructure these as the second element in the array that's returned. The two we care about are `loading` and `error`:

```javascript{4}
// web/src/pages/ContactPage/ContactPage.js

const ContactPage = () => {
  const [create, { loading, error }] = useMutation(CREATE_CONTACT)

  const onSubmit = (data) => {
    create({ variables: { input: data } })
    console.log(data)
  }

  return (...)
}
```

Now we know if the database call is still in progress by looking at `loading`. An easy fix for our multiple submit issue would be to disable the submit button if the response is still in progress. We can set the `disabled` attribute on the "Save" button to the value of `loading`:

```javascript{5}
// web/src/pages/ContactPage/ContactPage.js

return (
  // ...
  <Submit disabled={loading}>Save</Submit>
  // ...
)
```

It may be hard to see a difference in development because the submit is so fast, but you could enable network throttling via the Network tab Chrome's Web Inspector to simulate a slow connection:

<img src="https://user-images.githubusercontent.com/300/71037869-6dc56f80-20d5-11ea-8b26-3dadb8a1ed86.png" />

You'll see that the "Save" button become disabled for a second or two while waiting for the response.

Next, let's use Redwood's `Flash` system to let the user know their submission was successful. `useMutation` accepts an options object as a second argument. One of the options is a callback function, `onCompleted`, that will be invoked when the mutation successfully completes. We'll use that callback to add a message for the `Flash` component to display. Add the `Flash` component to the page and use the `timeout` prop to schedule the message's dismissal. (You can read the full documentation about Redwood's Flash system [here](https://redwoodjs.com/docs/flash-messaging-bus).)

```javascript{4,10,13-17,24}
// web/src/pages/ContactPage/ContactPage.js

// ...
import { Flash, useFlash, useMutation } from '@redwoodjs/web'
import BlogLayout from 'src/layouts/BlogLayout'

// ...

const ContactPage = () => {
  const { addMessage } = useFlash()

  const [create, { loading, error }] = useMutation(CREATE_CONTACT, {
    onCompleted: () => {
      addMessage('Thank you for your submission!', {
        style: { backgroundColor: 'green', color: 'white', padding: '1rem' }
      })
    },
  })

  // ...

  return (
    <BlogLayout>
      <Flash timeout={2000} />
      // ...
```

### Displaying Server Errors

Next we'll inform the user of any server errors. So far we've only notified the user of _client_ errors: a field was missing or formatted incorrectly. But if we have server-side constraints in place `<Form>` can't know about those, but we still need to let the user know something went wrong.

We have email validation on the client, but any good developer knows [_never trust the client_](https://www.codebyamir.com/blog/never-trust-data-from-the-browser). Let's add the email validation on the API as well to be sure no bad data gets into our database, even if someone somehow bypassed our client-side validation.

> Why don't we need server-side validation for the existence of name, email and message? Because the database is doing that for us. Remember the `String!` in our SDL definition? That adds a constraint in the database that the field cannot be `null`. If a `null` was to get all the way down to the database it would reject the insert/update and GraphQL would throw an error back to us on the client.
>
> There's no `Email!` datatype so we'll need to validate that on our own.

We talked about business logic belonging in our services files and this is a perfect example. Let's add a `validate` function to our `contacts` service:

```javascript{3,7-15,22}
// api/src/services/contacts/contacts.js

import { UserInputError } from '@redwoodjs/api'

import { db } from 'src/lib/db'

const validate = (input) => {
  if (input.email && !input.email.match(/[^@]+@[^.]+\..+/)) {
    throw new UserInputError("Can't create new contact", {
      messages: {
        email: ['is not formatted like an email address'],
      },
    })
  }
}

export const contacts = () => {
  return db.contact.findMany()
}

export const createContact = ({ input }) => {
  validate(input)
  return db.contact.create({ data: input })
}
```

So when `createContact` is called it will first validate the inputs and only if no errors are thrown will it continue to actually create the record in the database.

We already capture any existing error in the `error` constant that we got from `useMutation`, so we _could_ manually display an error box on the page somewhere containing those errors, maybe at the top of the form:

```html{4-9}
// web/src/pages/ContactPage/ContactPage.js

<Form onSubmit={onSubmit} validation={{ mode: 'onBlur' }}>
  {error && (
    <div style={{ color: 'red' }}>
      {"We couldn't send your message: "}
      {error.message}
    </div>
  )}
  // ...
```

> If you need to handle your errors manually, you can do this:
>
> ```javascript{3-8}
> // web/src/pages/ContactPage/ContactPage.js
> const onSubmit = async (data) => {
>   try {
>     await create({ variables: { input: data } })
>     console.log(data)
>   } catch (error) {
>     console.log(error)
>   }
> }
> ```

To get a server error to fire, let's remove the email format validation so that the client-side error isn't shown:

```html
// web/src/pages/ContactPage/ContactPage.js

<TextField
  name="email"
  validation={{
    required: true,
  }}
  errorClassName="error"
/>
```

Now try filling out the form with an invalid email address:

<img src="https://user-images.githubusercontent.com/300/80259406-5aee1900-863a-11ea-9b82-def3a4f3e162.png" />

It ain't pretty, but it works. Seeing a "GraphQL error" is not ideal, and it would be nice if the field itself was highlighted like it was when the inline validation was in place...

Remember when we said that `<Form>` had one more trick up its sleeve? Here it comes!

Remove the inline error display we just added (`{ error && ...}`) and replace it with `<FormError>`, passing the `error` constant we got from `useMutation` and a little bit of styling to `wrapperStyle` (don't forget the `import`). We'll also pass `error` to `<Form>` so it can setup a context:

```javascript{10,18-22}
// web/src/pages/ContactPage/ContactPage.js

import {
  Form,
  TextField,
  TextAreaField,
  Submit,
  FieldError,
  Label,
  FormError,
} from '@redwoodjs/forms'
import { Flash, useFlash, useMutation } from '@redwoodjs/web'
// ...

return (
  <BlogLayout>
    <Flash timeout={1000}>
    <Form onSubmit={onSubmit} validation={{ mode: 'onBlur' }} error={error}>
      <FormError
        error={error}
        wrapperStyle={{ color: 'red', backgroundColor: 'lavenderblush' }}
      />

      //...
)
```

Now submit a message with an invalid email address:

<img src="https://user-images.githubusercontent.com/300/80259553-c46e2780-863a-11ea-9441-54a9112b9ce5.png" />

We get that error message at the top saying something went wrong in plain english _and_ the actual field is highlighted for us, just like the inline validation! The message at the top may be overkill for such a short form, but it can be key if a form is multiple screens long; the user gets a summary of what went wrong all in one place and they don't have to resort to hunting through a long form looking for red boxes. You don't have to use that message box at the top, though; just remove `<FormError>` and the field will still be highlighted as expected.

> `<FormError>` has several styling options which are attached to different parts of the message:
>
> - `wrapperStyle` / `wrapperClassName`: the container for the entire message
> - `titleStyle` / `titleClassName`: the "Can't create new contact" title
> - `listStyle` / `listClassName`: the `<ul>` that contains the list of errors
> - `listItemStyle` / `listItemClassName`: each individual `<li>` around each error

### One more thing...

Since we're not redirecting after the form submits we should at least clear out the form fields. This requires we get access to a `reset()` function that's part of `react-hook-form` but we don't have access to it when using the simplest usage of `<Form>` (like we're currently using).

`react-hook-form` has a hook called `useForm()` which is normally called for us within `<Form>`. In order to reset the form we need to invoke that hook ourselves. But the functionality that `useForm()` provides still needs to be used in `Form`. Here's how we do that.

First we'll import `useForm`:

```javascript
// web/src/pages/ContactPage/ContactPage.js

import { useForm } from 'react-hook-form'
```

And now call it inside of our component:

```javascript{4}
// web/src/pages/ContactPage/ContactPage.js

const ContactPage = () => {
  const formMethods = useForm()
  //...
```

Finally we'll tell `<Form>` to use the `formMethods` we just instantiated instead of doing it itself:

```javascript{10}
// web/src/pages/ContactPage/ContactPage.js

return (
  <BlogLayout>
    <Flash timeout={1000}>
    <Form
      onSubmit={onSubmit}
      validation={{ mode: 'onBlur' }}
      error={error}
      formMethods={formMethods}
    >
    // ...
```

Now we can call `reset()` on `formMethods` after the success message is added to the Flash system:

```javascript
// web/src/pages/ContactPage/ContactPage.js

const [create, { loading, error }] = useMutation(CREATE_CONTACT, {
  onCompleted: () => {
    // addMessage...
    formMethods.reset()
  },
})
```

<img alt="Screenshot of Contact form with Flash success message" src="https://user-images.githubusercontent.com/44448047/93649232-1be9a700-f9d1-11ea-821c-7a69c626f50c.png">

> You can put the email validation back into the `<TextField>` now, but you should leave the server validation in place, just in case.

Here's the final `ContactPage.js` page:

```javascript
import {
  Form,
  TextField,
  TextAreaField,
  Submit,
  FieldError,
  Label,
  FormError,
} from '@redwoodjs/forms'
import { Flash, useFlash, useMutation } from '@redwoodjs/web'
import { useForm } from 'react-hook-form'
import BlogLayout from 'src/layouts/BlogLayout'

const CREATE_CONTACT = gql`
  mutation CreateContactMutation($input: CreateContactInput!) {
    createContact(input: $input) {
      id
    }
  }
`

const ContactPage = () => {
  const formMethods = useForm()
  const { addMessage } = useFlash()

  const [create, { loading, error }] = useMutation(CREATE_CONTACT, {
    onCompleted: () => {
      addMessage('Thank you for your submission!', {
        style: { backgroundColor: 'green', color: 'white', padding: '1rem' }
      })
      formMethods.reset()
    },
  })

  const onSubmit = (data) => {
    create({ variables: { input: data } })
    console.log(data)
  }

  return (
    <BlogLayout>
      <Flash timeout={1000} />
      <Form
        onSubmit={onSubmit}
        validation={{ mode: 'onBlur' }}
        error={error}
        formMethods={formMethods}
      >
        <FormError
          error={error}
          wrapperStyle={{ color: 'red', backgroundColor: 'lavenderblush' }}
        />
        <Label name="name" errorClassName="error">
          Name
        </Label>
        <TextField
          name="name"
          validation={{ required: true }}
          errorClassName="error"
        />
        <FieldError name="name" className="error" />

        <Label name="name" errorClassName="error">
          Email
        </Label>
        <TextField
          name="email"
          validation={{
            required: true,
          }}
          errorClassName="error"
        />
        <FieldError name="email" className="error" />

        <Label name="name" errorClassName="error">
          Message
        </Label>
        <TextAreaField
          name="message"
          validation={{ required: true }}
          errorClassName="error"
        />
        <FieldError name="message" className="error" />

        <Submit disabled={loading}>Save</Submit>
      </Form>
    </BlogLayout>
  )
}

export default ContactPage
```

That's it! [React Hook Form](https://react-hook-form.com/) provides a bunch of [functionality](https://react-hook-form.com/api) that `<Form>` doesn't expose. When you want to get to that functionality you can: just call `useForm()` yourself but make sure to pass the returned object (we called it `formMethods`) as a prop to `<Form>` so that the validation and other functionality keeps working.

> You may have noticed that the onBlur form validation stopped working once you started calling `useForm()` yourself. That's because Redwood calls `useForm()` behind the scenes and automaticaly passes it the `validation` prop that you gave to `<Form>`. Redwood is no longer calling `useForm()` for you so if you need some options passed you need to do it manually:
>
> ```javascript
> const formMethods = useForm({ mode: 'onBlur' })
> ```

The public site is looking pretty good. How about the administrative features that let us create and edit posts? We should move them to some kind of admin section and put them behind a login so that random users poking around at URLs can't create ads for discount pharmaceuticals.

## Administration

Having the admin screens at `/admin` is a reasonable thing to do. Let's update the routes to make that happen by updating the four routes starting with `/posts` to start with `/admin/posts` instead:

```html
// web/src/Routes.js

<Route path="/admin/posts/new" page={NewPostPage} name="newPost" />
<Route path="/admin/posts/{id:Int}/edit" page={EditPostPage} name="editPost" />
<Route path="/admin/posts/{id:Int}" page={PostPage} name="post" />
<Route path="/admin/posts" page={PostsPage} name="posts" />
```

Head to http://localhost:8910/admin/posts and our generated scaffold page should come up. Thanks to named routes we don't have to update any of the `<Link>`s that were generated by the scaffolds since the `name`s of the pages didn't change!

> On the last page we said we were going to set up an admin section **and** put it
> behind a login. So far, all we've done is updated the routes. Don't worry, we
> haven't forgotten! We will be setting up authentication in a [future step](/tutorial/authentication).

How about getting this thing out into the real world?

## Deployment

Part 4 of the video tutorial picks up here:

<div class="relative pb-9/16">
  <iframe class="absolute inset-0 w-full h-full" src="https://www.youtube.com/embed/UpD3HyuZkvY?rel=0" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture; modestbranding; showinfo=0" allowfullscreen></iframe>
</div>

The whole reason we started building Redwood was to make full-stack web apps easier to build and deploy on the Jamstack. You've seen what building a Redwood app is like, how about we try deploying one?

We've only got one change to make to the codebase to get it ready for deployment and we've got a generator to do it for us:

```terminal
yarn rw g deploy netlify
```

This creates a file at `/netlify.toml` which contains the commands and file paths that Netlify needs to know about to build a Redwood app.

Before we continue, make sure your app is fully committed and pushed to GitHub, GitLab, or Bitbucket. We're going to link Netlify directly to our git repo so that a simple push to `main` will re-deploy our site. If you haven't worked on the Jamstack yet you're in for a pleasant surprise!

> **NOTE:** Git initializes with `master`. Don't know how to rename `master` to `main`? If you're pushing to GitHub, you can follow these steps:
>
> ```plaintext{4,6}
> git init
> git add .
> git commit -m 'First commit'
> git branch -m main
> git remote add origin ...
> git push -u origin main
> ```

### Vercel (alternative deploy target)

Redwood officially supports multiple hosting providers (with even more on the way). Although this Tutorial continues with a focus on Netlify deployment and authentication with Netlify Identity, you can deploy to [Vercel](https://vercel.com/redwoodjs-core) instead. To do this, first complete "The Database" section below, but then use this [Vercel deploy walkthrough](https://redwoodjs.com/docs/deploy#redwood-deploy-configuration) in place of the following "Netlify" instructions. **Note**: Netlify Identity, used in upcoming "Authentication" section, won’t work on the Vercel platform.

### The Database

We'll need a database somewhere on the internet to store our data. We've been using SQLite locally, but that's a file-based store meant for single-user. SQLite isn't really suited for the kind of connection and concurrency requirements a production website will require. For this part of this tutorial, we will use Postgres. (Prisma currently supports SQLite, Postgres and MySQL.) Don't worry if you aren't familiar with Postgres, Prisma will do all the heavy lifting. We just need to get a database available to the outside world so it can be accessed by our app.

First we'll let Prisma know that we intend to use Postgres in addition to SQLite so it will build client libraries for both. Update the `provider` entry in `schema.prisma`:

```javascript
provider = ["sqlite", "postgresql"]
```

If you'd like to develop locally with Postgres, see the
[Local Postgres Setup](/docs/local-postgres-setup) guide.

> For now, you need to set up your own database, but we are working with various infrastructure providers to make this process simpler and more Jamstacky. Stay tuned for improvements in that regard!

There are several hosting providers where you can quickly start up a Postgres instance:

- [Heroku](https://www.heroku.com/postgres)
- [Digital Ocean](https://www.digitalocean.com/products/managed-databases)
- [AWS](https://aws.amazon.com/rds/postgresql/)

We're going to go with Heroku for now because it's a) free and b) easier to get started from scratch than AWS.

Head over to [Heroku](https://signup.heroku.com/) and create an account or log in. Then click that **Create a new app** button:

<img alt="Screen Shot 2020-02-03 at 3 22 36 PM" src="https://user-images.githubusercontent.com/300/73703866-438c3900-46a6-11ea-9a90-bdab2fed8bff.png">

Give it a name like "redwoodblog" if it's available. Go to the **Resources** tab and then click **Find more add-ons** in the **Add-ons** section:

<img alt="Screen Shot 2020-02-03 at 3 23 25 PM" src="https://user-images.githubusercontent.com/300/73703877-4e46ce00-46a6-11ea-87c0-079346f4d9b3.png">

And scroll down to **Heroku Postgres**:

<img alt="Screen Shot 2020-02-03 at 3 23 48 PM" src="https://user-images.githubusercontent.com/300/73703883-556ddc00-46a6-11ea-8777-ee27d2202e0e.png">

Click that and then on the detail page that comes up click the **Install Heroku Postgres** button that top right. On the next screen tell it you want to connect it to the app you just created, then click **Provision add-on**:

<img alt="Screen Shot 2020-02-03 at 3 24 15 PM" src="https://user-images.githubusercontent.com/300/73703930-64548e80-46a6-11ea-9f1b-e06a183834f4.png">

You'll be returned to your app's detail page. You should be on the **Resources** tab and see the Heroku Postgres add-on ready to go:

<img alt="Screen Shot 2020-02-03 at 3 24 43 PM" src="https://user-images.githubusercontent.com/300/73703951-6ae30600-46a6-11ea-8d9b-a900b7af2ac5.png">

Click the **Heroku Postgres** link to get to the detail page, then the **Settings** tab and finally the **View Credentials...** button. We did all the steps above so that we could copy the URI listed at the bottom:

<img alt="Screen Shot 2020-02-03 at 3 25 31 PM" src="https://user-images.githubusercontent.com/300/73703956-70405080-46a6-11ea-81f2-bed99ca4c4cc.png">

It will be really long and scroll off the right side of the page so make sure you copy the whole thing!

### Netlify

Now we're going to [create a Netlify account](https://app.netlify.com/signup) if you don't have one already. Once you've signed up and verified your email done just click the **New site from Git** button at the upper right:

<img src="https://user-images.githubusercontent.com/300/73697486-85f84a80-4693-11ea-922f-0f134a3e9031.png" />

Now just authorize Netlify to connect to your git hosting provider and find your repo. When the deploy settings come up you can leave everything as the defaults and click **Deploy site**.

Netlify will start building your app (click the **Deploying your site** link to watch the logs) and it will say "Site is live", but nothing will work. Why? We haven't told it where to find our database yet.

Go back to the main site page and then to **Settings** at the top, and then **Build & Deploy** > **Environment**. Click **Edit Variables** and this is where we'll paste the database connection URI we got from Heroku (note the **Key** is "DATABASE_URL"). After pasting the value, append `?connection_limit=1` to the end. The URI will have the following format: `postgres://<user>:<pass>@<url>/<db>?connection_limit=1`.

![Adding ENV var](https://user-images.githubusercontent.com/300/83188236-3e834780-a0e4-11ea-8cfa-790c2e335a92.png)

> When configuring a database, you'll want to append `?connection_limit=1` to the URI. This is [recommended by Prisma](https://www.prisma.io/docs/reference/tools-and-interfaces/prisma-client/deployment#recommended-connection-limit) when working with relational databases in a Serverless context.

Make sure to click the **Save** button. Now go over to the **Deploys** tab in the top nav and open the **Trigger deploy** dropdown on the right, then finally choose **Deploy site**:

![Trigger deploy](https://user-images.githubusercontent.com/300/83187760-835aae80-a0e3-11ea-9733-ff54969bba1f.png)

With a little luck (and SCIENCE) it will complete successfully! You can click the **Preview** button at the top of the deploy log page, or go back and click the URL of your Netlify site towards the top:

![Netlify URL](https://user-images.githubusercontent.com/300/83187909-bef57880-a0e3-11ea-97dc-e557248acd3a.png)

Did it work? If you see "Empty" under the About and Contact links then it did! Yay! You're seeing "Empty" because you don't have any posts in your brand new production database so head to `/admin/posts` and create a couple, then go back to the homepage to see them.

> If you view a deploy via the **Preview** button notice that the URL contains a hash of the latest commit. Netlify will create one of these for every push to `main` but will only ever show this exact commit, so if you deploy again and refresh you won't see any changes. The real URL for your site (the one you get from your site's homepage in Netlify) will show the latest deploy. See [branch deploys](#branch-deploys) below for more info.

If the deploy failed, check the log output in Netlify and see if you can make sense of the error. If the deploy was successful but the site doesn't come up, try opening the web inspector and look for errors. Are you sure you pasted the entire Postgres connection string correctly? If you're really, really stuck head over to the [Redwood Community](https://community.redwoodjs.com) and ask for help.

### Branch Deploys

Another neat feature of Netlify is _Branch Deploys_. When you create a branch and push it up to your repo, Netlify will build that branch at a unique URL so that you can test your changes, leaving the main site alone. Once your branch is merged to `main` then a deploy at your main site will run and your changes will show to the world. To enable Branch Deploys go to **Settings** > **Continuous Deployment** and under the **Deploy contexts** section click **Edit settings** and change **Branch deploys** to "All". You can also enable _Deploy previews_ which will create them for any pull requests against your repo.

![Netlify settings screenshot](https://user-images.githubusercontent.com/30793/90886476-c1016780-e3b2-11ea-851a-3014257484fd.png)

> You also have the ability to "lock" the `main` branch so that deploys do not automatically occur on every push—you need to manually tell Netlify to deploy the latest, either by going to the site or using the [Netlify CLI](https://cli.netlify.com/).

### A Note About DB Connections

In this tutorial, your lambda functions will be connecting directly to the Postgres database. Because Postgres has a limited number of concurrent connections it will accept, this does not scale very well. The proper solution is to put a connection pooling service in front of Postgres and connect to that from your lambda functions. To learn how to do that, see the [Connection Pooling](/docs/connection-pooling) guide.

We are working on making this process much easier, but keep it in mind before you deploy a Redwood app to production and announce it to the world.

## Authentication

"Authentication" is a blanket term for all of the stuff that goes into making sure that a user, often identified with an email address and password, is allowed to access something. Authentication can be [famously fickle](https://www.rdegges.com/2017/authentication-still-sucks/) to do right both from a technical standpoint and developer happiness standpoint.

But you know Redwood has your back! Login isn't something we have to write from scratch—it's a solved problem and is one less thing we should have to worry about. Today Redwood includes integrations to:

- [Auth0](https://auth0.com/)
- [Netlify Identity](https://docs.netlify.com/visitor-access/identity/)

We're going to demo a Netlify Identity integration in this tutorial since we're already deployed there and it's very easy to add to a Netlify site.

> There are two terms which contain a lot of letters, starting with an "A" and ending in "ation" (which means you could rhyme them if you wanted to) that become involved in most discussions about login:
>
> * Authentication
> * Authorization
>
> Here is how Redwood uses these terms:
>
> * **Authentication** deals with determining whether someone is who they say they are, generally by "logging in" with an email and password, or a third party OAuth provider like Google.
> * **Authorization** is whether a user (who has usually already been authenticated) is allowed to do something they want to do. This generally involves some combination of roles and permission checking before allowing access to a URL or feature of your site.
>
> This section of the tutorial focuses on **Authentication** only. We're currently working on integrating a simple and flexible role-based authorization system and once we release it we'll update the tutorial to include a walkthrough!

### Netlify Identity Setup

Assuming you've been following along, you already have a Netlify account and a site set up. If you'd be so kind, head to the **Identity** tab and click the **Enable Identity** button:

![Netlify Identity screenshot](https://user-images.githubusercontent.com/300/82271191-f5850380-992b-11ea-8061-cb5f601fa50f.png)

When the screen refreshes click the **Invite users** button and enter a real email address (they're going to send a confirmation link to it):

![Netlify invite user screenshot](https://user-images.githubusercontent.com/300/82271302-439a0700-992c-11ea-9d6d-004adef3a385.png)

We'll need to get that email confirmation link soon, but for now let's set up our app for authentication.

### Authentication Generation

There are a couple of places we need to add some code for authentication and lucky for us Redwood can do it automatically with a generator:

```terminal
yarn rw g auth netlify
```

The generator adds one file and modifies a couple others.

> Don't see any changes?
>
> For this to work you must be on version `0.7.0` or greater of Redwood. If you
> don't see any file changes, try
> [upgrading](/reference/command-line-interface#upgrade) your Redwood packages
> with `yarn rw upgrade`.

Take a look at the newly created `api/src/lib/auth.js` (usage comments omitted):

```javascript
// api/src/lib/auth.js

import { AuthenticationError } from '@redwoodjs/api'

export const getCurrentUser = async (decoded, { token, type }) => {
  return decoded
}

export const requireAuth = () => {
  if (!context.currentUser) {
    throw new AuthenticationError("You don't have permission to do that.")
  }
}
```

By default the authentication system will return only the data that the third-party auth handler knows about (that's what's inside the `jwt` object above). For Netlify Identity that's an email address, an optional name and optional array of roles. Usually you'll have your own concept of a user in your local database. You can modify `getCurrentUser` to return that user, rather than the details that the auth system stores. The comments at the top of the file give one example of how you could look up a user based on their email address. We also provide a simple implementation for requiring that a user be authenticated when trying to access a service: `requireAuth()`. It will throw an error that GraphQL knows what to do with if a non-authenticated person tries to get to something they shouldn't.

The files that were modified by the generator are:

* `web/src/index.js`—wraps the router in `<AuthProvider>` which makes the routes themselves authentication aware, and gives us access to a `useAuth()` hook that returns several functions for logging users in and out, checking their current logged-inness, and more.
* `api/src/functions/graphql.js`—makes `currentUser` available to the api side so that you can check whether a user is allowed to do something on the backend. If you add an implementation to `getCurrentUser()` in `api/src/lib/auth.js` then that is what will be returned by `currentUser`, otherwise it will return just the details the auth system has for the user. If they're not logged in at all then `currentUser` will be `null`.

We'll hook up both the web and api sides below to make sure a user is only doing things they're allowed to do.

### API Authentication

First let's lock down the API so we can be sure that only authorized users can create, update and delete a Post. Open up the Post service and let's add a check:

```javascript{4,17,24,32}
// api/src/services/posts/posts.js

import { db } from 'src/lib/db'
import { requireAuth } from 'src/lib/auth'

export const posts = () => {
  return db.post.findMany()
}

export const post = ({ id }) => {
  return db.post.findOne({
    where: { id },
  })
}

export const createPost = ({ input }) => {
  requireAuth()
  return db.post.create({
    data: input,
  })
}

export const updatePost = ({ id, input }) => {
  requireAuth()
  return db.post.update({
    data: input,
    where: { id },
  })
}

export const deletePost = ({ id }) => {
  requireAuth()
  return db.post.delete({
    where: { id },
  })
}

export const Post = {
  user: (_obj, { root }) => db.post.findOne({ where: { id: root.id } }).user(),
}
```

Now try creating, editing or deleting a post from our admin pages. Nothing happens! Should we show some kind of friendly error message? In this case, probably not—we're going to lockdown the admin pages altogether so they won't be accessible by a browser. The only way someone would be able to trigger these errors in the API is if they tried to access the GraphQL endpoint directly, without going through our UI. The API is already returning an error message (open the Web Inspector in your browser and try that create/edit/delete again) so we are covered.

> Note that we're putting the authentication checks in the service and not checking in the GraphQL interface (in the SDL files).
>
> Redwood created the concept of **services** as containers for your business logic which can be used by other parts of your application besides the GraphQL API. By putting authentication checks here you can be sure that any other code that tries to create/update/delete a post will fall under the same authentication checks. In fact, Apollo (the GraphQL library Redwood uses) [agrees with us](https://www.apollographql.com/docs/apollo-server/security/authentication/#authorization-in-data-models)!

### Web Authentication

Now we'll restrict access to the admin pages completely unless you're logged in. The first step will be to denote which routes will require that you be logged in. Enter the `<Private>` tag:

```javascript{3,12,16}
// web/src/Routes.js

import { Router, Route, Private } from '@redwoodjs/router'

const Routes = () => {
  return (
    <Router>
      <Route path="/contact" page={ContactPage} name="contact" />
      <Route path="/about" page={AboutPage} name="about" />
      <Route path="/" page={HomePage} name="home" />
      <Route path="/blog-post/{id:Int}" page={BlogPostPage} name="blogPost" />
      <Private unauthenticated="home">
        <Route path="/admin/posts/new" page={NewPostPage} name="newPost" />
        <Route path="/admin/posts/{id:Int}/edit" page={EditPostPage} name="editPost" />
        <Route path="/admin/posts/{id:Int}" page={PostPage} name="post" />
        <Route path="/admin/posts" page={PostsPage} name="posts" />
      </Private>
      <Route notfound page={NotFoundPage} />
    </Router>
  )
}

export default Routes
```

Surround the routes you want to be behind authentication and optionally add the `unauthenticated` attribute that lists the name of another route to redirect to if the user is not logged in. In this case we'll go back to the homepage.

Try that in your browser. If you hit http://localhost:8910/admin/posts you should immediately go back to the homepage.

Now all that's left to do is let the user actually log in! If you've built authentication before then you know this part is usually a drag, but Redwood makes it a walk in the park. Most of the plumbing was handled by the auth generator, so we get to focus on the parts the user actually sees. First, let's add a **Login** link that will trigger a modal from the [Netlify Identity widget](https://github.com/netlify/netlify-identity-widget). Let's assume we want this on all of the public pages, so we'll put it in the `BlogLayout`:

```javascript{4,7,22-26}
// web/src/layouts/BlogLayout/BlogLayout.js

import { Link, routes } from '@redwoodjs/router'
import { useAuth } from '@redwoodjs/auth'

const BlogLayout = ({ children }) => {
  const { logIn } = useAuth()

  return (
    <div>
      <h1>
        <Link to={routes.home()}>Redwood Blog</Link>
      </h1>
      <nav>
        <ul>
          <li>
            <Link to={routes.about()}>About</Link>
          </li>
          <li>
            <Link to={routes.contact()}>Contact</Link>
          </li>
          <li>
            <a href="#" onClick={logIn}>
              Log In
            </a>
          </li>
        </ul>
      </nav>
      <main>{children}</main>
    </div>
  )
}

export default BlogLayout
```

Try clicking the login link:

![Netlify Identity Widget modal](https://user-images.githubusercontent.com/300/82387730-aa7ef500-99ec-11ea-9a40-b52b383f99f0.png)

We need to let the widget know the URL of our site so it knows where to go to get user data and confirm they're able to log in. Back over to Netlify, you can get that from the Identity tab:

![Netlify site URL](https://user-images.githubusercontent.com/300/82387937-28430080-99ed-11ea-91b7-a4e10f14aa83.png)

You need the protocol and domain, not the rest of the path. Paste that into the modal and click that **Set site's URL** button. The modal should reload and now show a real login box:

![Netlify identity widget login](https://user-images.githubusercontent.com/300/82388116-97205980-99ed-11ea-8fb4-13436ee8e746.png)

Before we can log in, remember that confirmation email from Netlify? Go find that and click the **Accept the invite** link. That will bring you to your site live in production, where nothing will happen. But if you look at the URL it will end in something like `#invite_token=6gFSXhugtHCXO5Whlc5V`. Copy that (including the `#`) and appened it to your localhost URL: http://localhost:8910/#invite_token=6gFSXhugtHCXO5Whlc5Vg Hit Enter, then go back into the URL and hit Enter again to get it to actually reload the page. Now the modal will show **Complete your signup** and give you the ability to set your password:

![Netlify identity set password](https://user-images.githubusercontent.com/300/82388369-54ab4c80-99ee-11ea-920e-9df10ee0cac2.png)

Once you do that the modal should update and say that you're logged in! It worked! Click the X in the upper right to close the modal.

> We know that invite acceptance flow is less than ideal. The good news is that once you deploy your site again with authentication, future invites will work automatically—the link will go to production which will now have the code needed to launch the modal and let you accept the invite.

We've got no indication on our actual site that we're logged in, however. How about changing the **Log In** button to be **Log Out** when you're authenticated:

```javascript{7,23-24}
// web/src/layouts/BlogLayout/BlogLayout.js

import { Link, routes } from '@redwoodjs/router'
import { useAuth } from '@redwoodjs/auth'

const BlogLayout = ({ children }) => {
  const { logIn, logOut, isAuthenticated } = useAuth()

  return (
    <div>
      <h1>
        <Link to={routes.home()}>Redwood Blog</Link>
      </h1>
      <nav>
        <ul>
          <li>
            <Link to={routes.about()}>About</Link>
          </li>
          <li>
            <Link to={routes.contact()}>Contact</Link>
          </li>
          <li>
            <a href="#" onClick={isAuthenticated ? logOut : logIn}>
              {isAuthenticated ? 'Log Out' : 'Log In'}
            </a>
          </li>
        </ul>
      </nav>
      <main>{children}</main>
    </div>
  )
}

export default BlogLayout
```

`useAuth()` provides a couple more helpers for us, in this case `isAuthenticated` which will return `true` or `false` based on your login status, and `logOut()` which will log the user out. Now clicking **Log Out** should log you out and change the link to **Log In** which you can click to open the modal and log back in again.

When you *are* logged in, you should be able to access the admin pages again: http://localhost:8910/admin/posts

> If you start working on another Redwood app that uses Netlify Identity you'll need to manually clear out your Local Storage which is where the site URL is stored that you entered the first time you saw the modal. Local Storage is tied to your domain and port, which by default will be the same for any Redwood app when developing locally. You can clear your Local Storage in Chrome by going to the Web Inspector, the **Application** tab, and then on the left open up **Local Storage** and click on http://localhost:8910. You'll see the keys stored on the right and can delete them all.

One more touch: let's show the email address of the user that's logged in. We can get the `currentUser` from `useAuth()` and it will contain the data that our third party authentication library is storing about the currently logged in user:

```javascript{7,27}
// web/src/layouts/BlogLayout/BlogLayout.js

import { Link, routes } from '@redwoodjs/router'
import { useAuth } from '@redwoodjs/auth'

const BlogLayout = ({ children }) => {
  const { logIn, logOut, isAuthenticated, currentUser } = useAuth()

  return (
    <div>
      <h1>
        <Link to={routes.home()}>Redwood Blog</Link>
      </h1>
      <nav>
        <ul>
          <li>
            <Link to={routes.about()}>About</Link>
          </li>
          <li>
            <Link to={routes.contact()}>Contact</Link>
          </li>
          <li>
            <a href="#" onClick={isAuthenticated ? logOut : logIn}>
              {isAuthenticated ? 'Log Out' : 'Log In'}
            </a>
          </li>
          {isAuthenticated && <li>{currentUser.email}</li>}
        </ul>
      </nav>
      <main>{children}</main>
    </div>
  )
}

export default BlogLayout
```

![Logged in email](https://user-images.githubusercontent.com/300/82389433-05b2e680-99f1-11ea-9d01-456cad508c80.png)

> Check out the settings for Identity over at Netlify for more options, including allowing users to create accounts rather than having to be invited, add third party login buttons for Bitbucket, GitHub, GitLab and Google, receive webhooks when someone logs in, and more!

Believe it or not, that's it! Authentication with Redwood is a breeze and we're just getting started. Expect more magic soon!

> If you inspect the contents of `currentUser` you'll see it contains an array called `roles`. On the Netlify Identity dashboard you can give your user a collection of roles, which are just strings like "admin" or "guest". Using this array of roles you *could* create a very rudimentary role-based authentication system. Unless you are in dire need of this simple role checking, we recommend waiting for the Redwood solution, coming soon!

## Wrapping Up

You made it! If you really went through the whole tutorial: congratulations! If you just skipped ahead to this page to try and get a free congratulations: tsk, tsk!

That was potentially a lot of new concepts to absorb all at once so don't feed bad if all of it didn't fully sink in. React, GraphQL, Prisma, serverless functions...so many things! Even those of us working on the framework are heading over to Google multiple times per day to figure out how to get these things to work together.

As an anonymous Twitter user once mused: "If you enjoy feeling like both the smartest person on earth and the dumbest person in history within a span of 24 hours, programming may be the career for you!"

### What's Next?

Want to add some more features to your app? Check out some of our Cookbook recipies like [calling to a third party API](/cookbook/using-a-third-party-api) and [deploying an app without an API at all](/cookbook/disable-api-database). Have you grown out of SQLite and want to [install Postgres locally](/docs/local-postgres-setup)? We've also got lots of [guides](/docs/introduction) for more info on Redwood's internals.

### Roadmap

Check out our [Roadmap](https://redwoodjs.com/roadmap) to see where we're headed and how we're going to get there.
If you're interested in helping with anything you see, just let us know over on the [RedwoodJS Forum](https://community.redwoodjs.com/) and we'll be happy to get you set up.
We want to hit `1.0` by the end of the year. And with your help, we think we can do it!

### Help Us!

What did you think of Redwood? Is it the Next Step for JS frameworks? What can it do better? We've got a lot more planned. Want to help us build these upcoming features?

- [Open a PR](https://github.com/redwoodjs/redwood/pulls)
- [Write some docs](/docs/introduction)
- [Join the community](https://community.redwoodjs.com)

Thanks for following along. Now go out and build something amazing!
