<template>
  <ul>
    <learning-resource
      v-for="res in resources"
      :key="res.id"
      :id="res.id"
      :title="res.title"
      :description="res.description"
      :link="res.url"
    ></learning-resource>
  </ul>
</template>

<script>
import LearningResource from './LearningResource.vue';

export default {
  props: ['resources'  ],
  components: {
    LearningResource
  },
  methods : {
    func(){
      console.log(this.resources)
    }
  }
}
</script>

<style scoped>
ul {
  list-style: none;
  margin: 0;
  padding: 0;
  margin: auto;
  max-width: 40rem;
}
</style>