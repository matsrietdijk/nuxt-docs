---
title: "API : la méthode fetch"
description: La méthode `fetch` est utilisée pour remplir le store avant de faire le rendu de la page. C'est comme la méthode `asyncData` sauf qu'elle ne définit pas les données du composant.
---

# La méthode fetch

> La méthode `fetch` est utilisée pour remplir le store avant de rendre la page. C'est comme la méthode `asyncData` sauf qu'elle ne définit pas les données du composant.

- **Type :** `Function`

La méthode `fetch` est appelée avant chaque chargement de composant (**uniquement pour les composants de page**). Elle peut être appelée côté serveur ou avant de naviguer sur la route correspondante.

La méthode `fetch` reçoit l'objet [`context`](/api#context) comme premier argument, vous pouvez l'utiliser afin de récupérer des données et remplir le store. Pour rendre la méthode `fetch` asynchrone, **retournez une promesse**, Nuxt.js attendra la résolution de la promesse avant de faire le rendu du composant.

Exemple de `pages/index.vue` :

```html
<template>
  <h1>Étoiles : {{ $store.state.stars }}</h1>
</template>

<script>
export default {
  fetch ({ store, params }) {
    return axios.get('http://my-api/stars')
    .then((res) => {
      store.commit('setStars', res.data)
    })
  }
}
</script>
```

Vous pouvez également utiliser `async` / `await` pour rendre votre code plus propre :

```html
<template>
  <h1>Étoiles : {{ $store.state.stars }}</h1>
</template>

<script>
export default {
  async fetch ({ store, params }) {
    let { data } = await axios.get('http://my-api/stars')
    store.commit('setStars', data)
  }
}
</script>
```
