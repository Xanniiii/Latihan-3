<template>
    <div>
      <h1>Detail Artikel</h1>
      <h2>{{ article.title }}</h2>
      <p>{{ article.content }}</p>
    </div>
  </template>
  
  <script>
  export default {
    async asyncData({ params }) {
      const response = await fetch('https://s.id/sbnews');
      const articles = await response.json();
      const article = articles.find(a => a.id === params.id);
      return { article };
    }
  };
  </script>
  