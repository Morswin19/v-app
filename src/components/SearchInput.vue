<template>
  <div class="searchWrapper">
      <label for="search">Search: </label>
      <input
        id="search"
        name="search"
        v-model="searchValue"
        @input="handleInput"
      />
    </div>
</template>

<script>
export default {
  name: 'SearchInput',
};
</script>

<style lang="sass" scoped>
    .searchWrapper
        display: flex
        flex-direction: column
        width: 250px
        input
            height: 20px
            width: 100%
            border: none
            border-bottom: 2px solid blue
            background: none
</style>
