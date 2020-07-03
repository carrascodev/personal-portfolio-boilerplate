<template>
<BContainer>
  <div>
    <b-card v-if="articles" v-for="article in articles"
      :key="article.title"
      :title="article.title"
      :img-src="article.img"
      img-alt="Image"
      img-top
      tag="article"
      style="max-width: 20rem;"
      class="mb-2"
    >
      <b-card-text>
        {{article.description}}
      </b-card-text>

      <b-button :to="article.path" variant="primary">Read more</b-button>
    </b-card>
  </div>
</BContainer>
</template>

<script lang="ts">

  import Vue from "vue";
  import Component from "nuxt-class-component";
  import {Article} from "~/models/article";

    @Component
    export default class Articles extends Vue {


      async asyncData(context: any) {
        console.log("asyncData setting")
        return {
          articles: await context.$content('articles').without(['body']).fetch() as Article[]
        }
      }




    }
</script>

<style scoped>

</style>
