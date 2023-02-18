# Séance 5 : Cycle de vie et API

{% hint style="info" %}

Cette séance est la traduction/adaptation de la documentation officielle se trouvant ici : [https://vuejs.org/guide/essentials/lifecycle.html](https://vuejs.org/guide/essentials/lifecycle.html)

{% endhint %}

Chaque instance d'un composant Vue passe par une série d'étapes d'initialisation lorsqu'elle est créée - par exemple, il faut paramétrer l'observation des données, compiler le template, monter l'instance sur le DOM, et le mettre à jour lorsque les données changent. En cours de route, des fonctions appelées hooks du cycle de vie sont également exécutées, donnant la possibilité à l'utilisateur d'ajouter son propre code à des étapes spécifiques.

Ci-dessous figure le diagramme du cycle de vie d'une instance.

[!https://fr.vuejs.org/assets/lifecycle.6903e504.png](Cycle de vie d'un composant Vue)

Chaque case rouge est un moment où il est possible d'intéragir avec le composant.

## Enregistrement des hooks du cycle de vie

Par exemple, le hook `onMounted` peut être utilisé pour exécuter du code après que le composant ait terminé son rendu initial et créer les nœuds du DOM (sur la case route `mounted` du schéma ci-dessus):

```javascript
<script setup>
import { onMounted } from 'vue'

onMounted(() => {
  console.log(`the component is now mounted.`)
})
</script>
```

Il y a également d'autres hooks qui peuvent être appelés à différentes étapes du cycle de vie de l'instance, dont les plus couramment utilisés sont onMounted, onUpdated, et onUnmounted.

Il peut être intéressant d'utiliser ce hook pour effectuer des actions lorsque le composant est monté, mis à jour ou démonté. Par exemple, onMounted peut être utilisé pour récupérer des données depuis une API, et onUnmounted pour annuler les abonnements aux événements.

## Accès aux données depuis un appel API

{% hint style="info" %}

Les appels API peuvent se faire à chaque fois que nécessaire, dans des méthodes, dans des hooks, ...

{% endhint %}