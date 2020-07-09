<template>
  <section id="projects">
    <Banner title="Projects"/>
    <b-container>
      <b-row v-for="(n, i) in numOfRows(cards.length)" :key="i">
        <b-col v-for="(card,index) in getNextCards(i)" md="4" :key="index">
          <ProjectCard :card="card"/>
        </b-col>
      </b-row>
    </b-container>
  </section>
</template>

<script lang="ts">
  import Vue from "vue";
  import Component from "nuxt-class-component";

  @Component
  export default class Projects extends Vue {

    async asyncData(context: any) {
      let cards = await context.$content("projects").only(["slug", "cover", "title","path"]).fetch()

      console.log(cards)
      return {
        cards
      }
    }

    numOfRows(len: number) {
      let rounded = Math.round(len / 3);
      rounded = rounded == 0 ? 1 : rounded;
      return rounded;
    }

    hasKey(num: number) {
      return num < this.$data.cards.length - 1
    }

    getNextCards(index: number) {
      let lastIndex = index + 2;

      while (lastIndex > this.$data.cards.length-1) {
        lastIndex--;
      }

      console.log(index)
      console.log(lastIndex)
      console.log(this.$data.cards.slice(index, lastIndex+1));

      return this.$data.cards.slice(index, lastIndex+1);

    }

  }
</script>

<style scoped>

</style>
