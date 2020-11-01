<template>
  <div class="itemWrapper">
        <div :style="style" class="item"></div>
  </div>
</template>

<script>
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
      photo: this.item.webformatURL,
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
  .itemWrapper
    // margin: 10px
    .item
        width: 25vw
        width: 300px
        height: 300px
        background-size: cover
        background-repeat: no-repeat
        background-position: 50%
        box-shadow: 5px 5px 10px 5px rgba(0,0,0,0.15)
        cursor: pointer
</style>
