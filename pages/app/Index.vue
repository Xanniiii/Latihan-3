<template>
    <div>
      <h1>Daftar Artikel</h1>
      <ul>
        <li v-for="article in articles" :key="article.id">
          <nuxt-link :to="'/artikel/' + article.id">{{ article.title }}</nuxt-link>
        </li>
      </ul>
    </div>
  </template>
  
  <script>
  export default {
    async asyncData({ params }) {
      const response = await fetch('https://s.id/sbnews');
      const articles = await response.json();
      return { articles };
    }
  };
  </script>
  