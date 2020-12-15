<template>
  <div>
    <LikeHeader>
      <template v-slot:title>
        <h1>トータルのいいね数</h1>
      </template>
      <template v-slot:num>
        <h2>{{ number }}</h2>
      </template>
    </LikeHeader>

    <LikeNumber :total-number="number" v-on:my-click="number = $event"></LikeNumber>
    <LikeNumber :total-number="number" v-on:my-click="number = $event"></LikeNumber>
  </div>
</template>


<script>
import LikeHeader from "./components/LikeHeader.vue";

export default {
  data(){
    return {
     number: 14
    };
  },
  components: {
    LikeHeader
  }
};
</script>

<style scoped>
  div{
    border:  1px solid blue;
  }
</style>
