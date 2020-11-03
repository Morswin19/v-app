<template>
  <div class="claimWrapper">
    <h1 class="claim">Photonia</h1>
    <p class="description">
        Open your mind for billions of incredible photos
    </p>
    <p class="description">
        Search for your favourite subject
    </p>
  </div>
</template>

<script>
export default {
  name: 'Claim',
};
</script>

<style lang="sass" scoped>
    .claimWrapper
        display: flex
        flex-direction: column
        justify-content: center
        align-items: center
        color: #FFFFFF
        border-radius: 40px
        padding: 30px
        text-align: center
        .claim
            font-size: 50px
            margin-bottom: 20px
        .description
            font-size: 15px
            margin-bottom: 15px

</style>
