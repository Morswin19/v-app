<template>
  <div>
    <div v-for="item in results" :key="item.id">
        <div :style="style" class="item"></div>
    </div>
  </div>
</template>

<script>
// console.log(this.photo);

export default {
  name: 'Item',
  props: {
    item: {
      type: Object,
      required: true,
    },
  },
  data() {
    return {
      photo: this.item.largeImageURL,
    };
  },
  computed: {
    style() {
      return `background-image: url("${this.photo}")`;
    },
  },
};
</script>

<style lang="sass" scoped>
    .item
        width: 200px
        height: 300px
        background-size: cover
        background-repeat: no-repeat
        background-position: 50%
</style>
