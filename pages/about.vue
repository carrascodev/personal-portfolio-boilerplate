<template>
  <section id="about">
    <Banner/>
    <div class="container-lg">
      <b-row>
        <b-col md="8">
          <h2>Personal Summary</h2>
          <p>{{about.profileDesc}}</p>
        </b-col>
        <b-col md="4" class="text-center drag-lg-top">
          <img src="/author.jpg" class="img-fluid w-75 rounded img-border shadow-sm"/>
        </b-col>
      </b-row>
      <b-row>
        <b-col md="12">
          <h3 style="text-transform: uppercase">Experiences</h3>
        </b-col>
      </b-row>
      <span :load="count = 0"/>
      <b-row v-for="(n,i) in numOfRows(this.$data.about.experiences.length)">
        <b-col md="6" v-if="i+count < about.experiences.length">
          <p class="h5">{{about.experiences[i+count].role}}</p>
          <p><span class="h6">{{about.experiences[i+count].company}}</span>,
            <span>{{about.experiences[i+count].period}}</span></p>
          <p class="desc-pre">{{about.experiences[i+count].desc}}</p>
        </b-col>
        <span :load="count++"/>
        <b-col v-if="i+count < about.experiences.length">
          <p class="h5">{{about.experiences[i+count].role}}</p>
          <p><span class="h6">{{about.experiences[i+count].company}}</span>,
            <span>{{about.experiences[i+count].period}}</span></p>
          <p class="desc-pre">{{about.experiences[i+count].desc}}</p>
        </b-col>
      </b-row>
      <hr>
      <b-row>
        <b-col md="12">
          <h3 style="text-transform: uppercase">Education</h3>
        </b-col>
      </b-row>
      <span :load="count = 0"/>
      <b-row v-for="(n,i) in numOfRows(about.education.length)">
        <b-col md="6" v-if="i+count < about.experiences.length">
          <p class="h5">{{about.education[i+count].course}}</p>
          <p><span class="h6">{{about.education[i+count].institution}}</span>,
            <span>{{about.education[i+count].period}}</span></p>
        </b-col>
        <span :load="count++"/>
        <b-col v-if="i+count < about.education.length">
          <p class="h5">{{about.education[i+count].course}}</p>
          <p><span class="h6">{{about.education[i+count].institution}}</span>,
            <span>{{about.education[i+count].period}}</span></p>
        </b-col>
      </b-row>
      <hr>
      <b-row>
        <h3 style="text-transform: uppercase">Skills</h3>
      </b-row>
      <b-row>
        <b-col md="4">
          <span v-for="(skill, i) in about.skills" :key="i">
            <b-badge variant="dark" style="font-size: 16px; margin-top: 5px" :ref="skill.name">{{skill.name}}</b-badge>
            <span></span>
          </span>
          <b-tooltip v-for="(skill, i) in about.skills" :target="skill.name" :key="i">
            {{getSkillLevel(skill.level)}}
          </b-tooltip>
        </b-col>
      </b-row>
    </div>
  </section>
</template>

<script lang="ts">
  import Vue from "vue";
  import Component from "nuxt-class-component";

  @Component
  export default class About extends Vue {
    async asyncData(context: any) {
      console.log("asyncData set")
      return {
        about: await context.$content('about').fetch(),
        count: 0
      }
    }

    numOfRows(num: number) {
      return Math.round(num / 2);
    }


    log(text: any) {
      console.log(text);
    }

    getSkillLevel(level: number) {
      let txt = "";
      for (let i = 0; i < level; i++) {
        txt += "<font-awesome-icon :icon=\"['fas', 'star']\" style=\"font-size: 12px\"/>";
      }

      return txt;
    }

  }
</script>

<style scoped>
  .drag-lg-top {
    margin-top: -150px;
  }

  .img-border {
    border: 7px solid white;
  }

  .row {
    margin-top: 25px;
  }

  .desc-pre {
    white-space: pre;
    word-wrap: break-word;
    font-family: inherit;
  }

</style>
