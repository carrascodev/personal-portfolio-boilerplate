<template>
  <div id="project-page">

    <Banner :title="page.title"/>
    <div class="container">
      <b-row v-for="(image, i) in page.images" :key="i" style="margin-top: 10px">
        <b-col md="6">
          <img :src="image" class="img-fluid rounded">
        </b-col>
        <b-col id="project-body" v-if="i == 0">
            <nuxt-content :document="page"></nuxt-content>
        </b-col>
      </b-row>
    </div>
  </div>

</template>

<script lang="ts">
  import Vue from "vue";
  import Component from "nuxt-class-component";

  @Component
  export default class ProjectPage extends Vue {

    body: HTMLElement | null = null;

    async asyncData(context: any) {
      return {
        page: await context.$content('projects', context.params.slug).fetch()

      }
    }

    mounted() {
      if(this.$data.page.stickyText) {
        window.onscroll = () => this.onScroll();
      }
    }

    onScroll() {
      if(!this.body)
        this.body = document.getElementById("project-body");

      const sticky = this.body?.offsetTop ?? 0;
      if(window.pageYOffset > sticky) {
        this.body?.classList.add("sticky");
      } else {
        this.body?.classList.remove("sticky");
      }
    }
  }
</script>

<style scoped>
  .container {
    display: block;
    margin-top: 50px;
  }

  .sticky {
    position: fixed;
    top: 0;
    padding-top: 10em;
    margin-left: 35em;
    width: 40%;
  }

</style>
