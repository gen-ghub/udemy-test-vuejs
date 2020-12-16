<template>
  <div>
    <slot name="title" :user="user" text="text"></slot>
    <p>いいねの数</p>
    <slot></slot>
    <slot name="num"></slot>

  </div>

</template>

<script>
export default {
  data(){
    return{
      user:{
        firstName:"Jack",
        lastName: "Donald"
      }
    };
  }
};
</script>

