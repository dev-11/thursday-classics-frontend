<template>
<div>
    <img v-bind:src="this.poster"/>
</div>
</template>

<script>
export default {
  name: "Card",
  data() {
    return {
        title: this.info[0],
        poster: this.info[1]
    };
  },
  props: {
    info: Object
  },
};
</script>

<style>
</style>