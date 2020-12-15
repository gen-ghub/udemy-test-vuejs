<template>
  <div>
    <slot name="title"></slot>
    <p>いいねの数</p>
    <slot name="num"></slot>
    
  </div>

</template>

<script>
export default {
  props: ["headerText"]
}
</script>

