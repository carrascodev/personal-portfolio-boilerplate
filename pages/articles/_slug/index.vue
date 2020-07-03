<template>
  <div class="container">
      <h1>{{page.title}}</h1>
      <nuxt-content :document="page"/>
  </div>
</template>

<script lang="ts">
  import Vue from "vue";
  import Component from "nuxt-class-component";

  @Component
  export default class ArticlePage extends Vue {
    async asyncData(context: any) {

      return {
        page: await context.$content('articles', context.params.slug).fetch()
      }
    }
  }
</script>

<style scoped>
  .container {
    display: block;
  }

</style>
