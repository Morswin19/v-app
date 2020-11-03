<template>
  <div class="mainImage"></div>
</template>

<script>
export default {
  name: 'MainImage',
};
</script>

<style lang="sass" scoped>
    .mainImage
        position: fixed
        z-index: -1
        width: 100%
        height: 100vh
        background-image: url('../assets/background14.jpg')
        background-repeat: no-repeat
        background-size: cover
        background-position: 50% 0%
        top: 0
        left: 0

    .mainImage::after
        content: ''
        background: rgba(0,0,0, 0.2)
        position: absolute
        top: 0
        ledt: 0
        z-index: 1
        width: 100%
        height: 100vh
</style>
