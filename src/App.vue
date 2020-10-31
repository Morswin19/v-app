<template>
  <div class="app">
    <div class='headWrapper'>
    <div>Logo</div>
    <div class="nav">
      <router-link to="/">photos</router-link>
      <router-link to="/about">about</router-link>
    </div>
    </div>
    <router-view />
  </div>
</template>

<style lang="sass">
  @import url('https://fonts.googleapis.com/css2?family=Montserrat:wght@300;400;500;600;900&display=swap')
  *
    box-sizing: border-box
    margin: 0
    padding: 0

  body
    font-family: 'Montserrat', sans-serif
    font-weight: 500

  .headWrapper
    position: fixed
</style>
