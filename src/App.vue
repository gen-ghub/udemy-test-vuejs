<template>
  <div>
    <LikeHeader>
      <h2>皆さん</h2>
      <template>
        <h1>トータルのいいね数</h1>
      </template>

      <template v-slot:num>
        <h2>{{ number }}</h2>
      </template>
    </LikeHeader>

    <LikeNumber
      :total-number="number"
      v-on:my-click="number = $event"
    ></LikeNumber>
    <LikeNumber
      :total-number="number"
      v-on:my-click="number = $event"
    ></LikeNumber>
    <button @click="currentComponent = 'Home'">Home</button>
    <button @click="currentComponent = 'About'">About</button>
    <keep-alive>
      <component :is="currentComponent"></component>
    </keep-alive>
  </div>
</template>

<script>
import LikeHeader from "./components/LikeHeader.vue";
import About from "./components/About.vue";
import Home from "./components/Home.vue";

export default {
  data() {
    return {
      number: 14,
      currentComponent: "Home",
    };
  },
  components: {
    LikeHeader,
    About,
    Home,
  },
};
</script>

<style scoped>
div {
  border: 1px solid blue;
}
</style>
