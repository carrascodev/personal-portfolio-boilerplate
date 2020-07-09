<template>
  <div class="slider-area">
    <div style="padding-top: 15vh"></div>
    <div v-if="hasTitle()" class="h2 text-center" id="banner-title">{{title}}</div>
    <div style="padding-top: 15vh"></div>
  </div>
</template>

<script lang="ts">
  import Vue from "vue";
  import Component from "nuxt-class-component"
  import {Prop} from "vue-property-decorator";

  @Component
  export default class Banner extends Vue {
      @Prop(String)
      readonly title: string;


      hasTitle() {
        return this.title;
      }


  }
</script>

<style scoped>

  .slider-area {
    width: 100%;
    height: 100%;
    background: rgba(0, 0, 0, 0.5) url('/intro-bg.jpg') center;
  }

  .row-padding {
    padding-top: 30vh;
  }

  #banner-title  {
    color: #fff;
    text-shadow: rgba(0, 0, 0, 0.6) 2px 2px 3px;
  }

</style>
