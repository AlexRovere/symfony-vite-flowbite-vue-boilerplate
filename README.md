# Symfony + Vite ⚡️

Configuration d'un projet **Symfony 6.4 LTS** avec **Vite** et support **Vue.js 3**.  
Profitez du hotreload pour CSS, JS et Twig, tout en gardant une stack légère et moderne. 🚀

## ✅ Avantages

- 🔥 **Hotreload** : CSS / JS / Twig se rechargent automatiquement
- ✅ **Vue 3** fonctionne parfaitement
- 📦 Symfony **6.4 LTS**
- 🪶 Plus léger qu'avec Webpack Encore

## ❌ Inconvénients

- Installation complexe sur un projet existant (surtout si déjà configuré avec `symfony/webpack-encore-bundle`)

## ⚙️ Installation

### Dépendances

```bash
composer install
npm install
npm install -g concurrently   # optionnel (pour lancer symfony & vite en parallèle)
```

### Base de données

Configurer votre fichier `.env.dev.local` :

```env
DATABASE_URL="mysql://root:@127.0.0.1:3306/sortir?serverVersion=8.0.32&charset=utf8mb4"
```

Puis exécuter :

```bash
symfony console doctrine:database:create
symfony console doctrine:migrations:migrate
```

## 🚀 Lancer l'application

### Avec concurrently

```bash
npm run serve
```

### Sinon (2 terminaux séparés)

```bash
symfony serve
npm run dev
```

## 🖼️ Gérer les images

Placer vos images dans `public/images`.  
Exemple dans Twig :

```twig
<img src="{{ asset('images/logo.jpg') }}" alt="Logo">
```

## 📜 Ajouter un script sur une page spécifique

1. Dans `vite.config.js`, ajouter votre script dans `build.rollupOptions.input` :

```js
input: {
   app: './assets/app.js',
   address: './assets/address.js', // exemple
}
```

2. Dans votre template Twig :

```twig
{% block javascripts %}
   {{ parent() }}
   {{ vite_entry_script_tags('address') }}
{% endblock %}
```

⚠️ **Important** : toujours mettre `{{ parent() }}` pour récupérer le script de base (ex: Tailwind).  
Sinon, votre bloc écrase complètement le précédent.

## 🖥️ Utiliser un composant Vue 3

### Exemple composant `Hello.vue` (dans `assets/vue/controllers`)

```vue
<template>
  <div class="bg-blue-500 p-8">Hello {{ twigProps }}</div>
</template>

<script setup>
defineProps({
  twigProps: String,
});
</script>
```

### Dans un template Twig

```twig
{{ vue_component('Hello', { 'twigProps': propsFromTwig }) }}
```

- **1er paramètre** : nom du fichier `.vue`
- **2ème paramètre** (optionnel) : props transmises depuis Twig

## 📚 Documentation

- [Symfony](https://symfony.com/doc/current/index.html)
- [Vite](https://vitejs.dev/)
- [Vue 3](https://vuejs.org/)

🎉 **Amusez-vous bien avec Vue & Symfony + Vite !**
