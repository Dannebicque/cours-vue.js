# Séance 1 : Concepts et installation

## Préambule

{% hint style="info" %}
Ce cours se base sur la version 3 de Vue.js. Attention vous trouverez beaucoup d'exemple en Vue.js 2 sur les forums et sites d'aide.
{% endhint %}

La documentation officielle se trouve ici sur le lien suivant

{% embed url="https://vuejs.org/" %}
Site officiel de Vue.js 3
{% endembed %}

## Présentation des concepts de Vue.js



## Installation et démarrage d'une nouveau projet.

Assurez vous de disposer de nodeJs et de npm fonctionnels, testez avec la commande ci-dessous

`npm --version`

Pour créer un nouveau projet, tapez la commande suivante :

```
npm init vue@latest
```

{% hint style="info" %}
Lors de la première execution, la commande va vous proposer d'installer create-vue. Confirmez la proposition
{% endhint %}

Répondez aux différentes questions. Par défaut mettez toutes les questions sur non, sauf "**Add Vue Router for single Page Application development**" que vous pouvez mettre sur **yes.**

Executez les commandes suivantes :

```
  cd vue-lp
  npm install
  npm run dev
```

La première commande accède au répertoire, la deuxième installe toute les dépendances (comme `composer install` avec PHP/Syfmony), la dernière lance le serveur qui va s'occuper de compiler les fichiers et rendre l'application "Vue.js" utilisable dans tous les navigateurs.

Vous devriez voir un message vous proposant l'url de votre projet "compilé". Ouvrez-là et vous devriez avoir une page similaire à celle ci-dessous :&#x20;



<figure><img src=".gitbook/assets/Capture d’écran 2023-02-05 à 18.35.51.png" alt=""><figcaption><p>Page d'accueil suite à la première installation d'un projet Vue.js</p></figcaption></figure>

## Premier exemple

## Premières manipulations.

Dans le composant App.vue qui est créé par défaut, et qui est le point d'entrée de votre application, nous allons faire les premiers tests.

Nous allons définir une liste de 3 éléments, par exemple :

```html
<ul>
  <li>Note sur Symfony : 19</li>
  <li>Note en intégration : 12</li>
  <li>Note en réseau : 14</li>
</ul>
```

Si on souhaite rendre cette liste "dynamique", on peut définir des variables pour les notes. La syntaxe est identique à Twig pour les variables...

```html
<ul>
  <li>Note sur Symfony : {{ symfony }}</li>
  <li>Note en intégration : {{ integration }}</li>
  <li>Note en réseau : {{ reseau }}</li>
</ul>
```

Si vous testez de nouveau ce code, vous aurez une erreur car les variables n'existent pas. Nous devons les définir.

Pour cela, dans la partie javascript de notre fichier App.vue, nous allons définir une "entrée" data, qui va contenir nos valeurs.

La déclaration pourrait être (en vue2 ou vue3 "classique":

```javascript
<script>
export default {
  name: 'App',
  data: () => {
    return {
      symfony: 6,
      integration: 2,
      reseau: 8,
    }
  },
}
</script>
```

{% hint style="warning" %}
Nous utiliserons la notation qui est préconisée avec la version 3 de Vue.js le "mode Composition API" ([https://vuejs.org/guide/extras/composition-api-faq.html](https://vuejs.org/guide/extras/composition-api-faq.html))
{% endhint %}

Notre code dans la partie script se résume donc à :

```javascript
<script setup>
const symfony = 18
const integration = 16
const reseau = 13
</script>
```

## Reprenons depuis le début

### Analysons notre répertoire de projet&#x20;

* **node\_module** : contient toutes les dépendances de notre projet. Il est créé par la commande `npm install`. Il ne faut rien modifier dans ce dossier, et ne jamais le gérer avec git. Son équivalent dans Symfony est vendor.
* **public** : c'est le repertoire "public", qui contient les éléments type images, favicon, les fichiers uploadés par vos utilisateurs, ... Il a le même rôle que "public" dans symfony.
* **src** : c'est note répertoire de travail, la très grande majorité de notre code se trouvera dans ce dossier.
* **index.html** : c'est le fichier html de base qui est affiché dans le navigateur et qui va intégrer nos composants Vue.js. Sa syntaxe est décrite par la suite.
* **package.json** (et son package-lock.json), sont la liste des dépendants installées, c'est l'équivalent du composer.json pour le back.
* **vite.config.js** : c'est l'automatisateur de tâches (comme gulp ou webpack, Vue.js 3 recommande l'usage de [Vite](https://vitejs.dev/) qui est plus rapide et performant). Nous reviendrons sur ce fichier en BUT3. Il récupère tous les éléments du dossier src/, va les traduires en du JavaScript compréhensible par les navigateurs et en faire un seul et unique point d'entrée.

#### Détail du fichier index.html

{% code title="index.html" lineNumbers="true" %}
```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8">
    <link rel="icon" href="/favicon.ico">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Vite App</title>
  </head>
  <body>
    <div id="app"></div>
    <script type="module" src="/src/main.js"></script>
  </body>
</html>

```
{% endcode %}

* ligne 10 : ce élément, avec un id "app" est l'élément qui va pouvoir recevoir notre code, nous le verrons avec le fichier main.js. Vous pourriez avoir plusieurs balises recevant plusieurs parties Vue.js. Vous pourriez aussi avoir un habillage HTML défini dans cette page et un "morceau" géré par Vue.js.
* ligne 11 : C'est l'intégration du fichier main.js qui va contenir tout notre code JavaScript et les composants Vue.js.

#### Détails du repertoire src/

* **assets** : votre CSS/SCSS ... global à votre projet. Les logos et images du site.
* **components** : nos composants Vue.js, des parties d'une page, qui seront assemblés pour faire votre page globale.
* **router** : contiendra nos routes de notre site, le lien entre l'URL, les pages Vue.js.
* **views** : les pages "Vue.js", qui assemblent les composants.
* **App.vue** : notre composant principal, décrit par la suite
* **main.js** : le fichier utilisé par ViteJs pour faire le lien entre les fichiers Vue.js, et la page index.html.

Cette structure est la base, vous pouvez l'organiser autrement, et ajouter toute la décomposition nécessaire.

#### Détail du fichier App.vue

Ce fichier est construit selon la structure "classique" de Vue.js, décrite dans la partie suivante.

```javascript
<script setup>
  const symfony = 18
  const integration = 16
  const reseau = 13
</script>

<template>
  <ul>
    <li>Note sur Symfony : {{ symfony }}</li>
    <li>Note en intégration : {{ integration }}</li>
    <li>Note en réseau : {{ reseau }}</li>
  </ul>
</template>

<style scoped>
li {
  color: red;
}
</style>

```

#### Structure d'un fichier Vue.js (.vue)

Si on utilise vue en mode "composant" (c'est à dire avec des fichiers .vue) et en mode Composition API, un fichier .vue à les éléments suivants :&#x20;

* template : qui contient le code HTML de votre composant (une partie de votre page). Ce code peut exploiter lui même d'autres composants Vue.js. La balise template doit contenir un seul enfant dans le dom.
* script : qui va contenir votre code JavaScript : les variables, les méthodes, les différents imports...
* style : optionnel, pour contenir le CSS propre au composant.

#### Détail du fichier main.js

{% code lineNumbers="true" %}
```javascript
import { createApp } from 'vue'
import App from './App.vue'
import router from './router'

import './assets/main.css'

const app = createApp(App)

app.use(router)

app.mount('#app')

```
{% endcode %}

C'est le fichier clé de votre application, l'équivalent du index.php de Symfony, car c'est lui qui contrôle tout ce qui va se passer, c'est le point d'entrée. c'est dans ce fichier que l'on peut instancier des dépendances globalements (comme router ici)

* **Ligne 1** : Import de Vue.js, et du composant createApp pour construire l'application (utilisé ligne 7)
* **Ligne 2** : On importe notre composant Vue.js App.Vue pour pouvoir l'exploiter dans notre fichier, et ici l'injecter dans la page ligne 7
* **Ligne 3** : le router pour gérer nos routes. On l'associe à notre application (ligne 9)
* **Ligne 5** : on importe notre CSS (ou autre), pour l'appliquer globalement au projet. Si c'est du Scss/Sass, ViteJs se chargera de le compiler en CSS.
* **Ligne 7** : on instancie notre application Vue.js avec le composant App (importé ligne 2)
* **Ligne 9** : on associe à notre application "app", le router, ce qui nous permettra de l'utiliser partout.
* **Ligne 11** : Cette ligne vient "injecter" notre application vue, dans la page html (index.html), et très exaxctement dans la balise avec l'id "app"

### Templates

#### Variable, structuration, données (simple variable, objet json, quelques exemples)

###

\