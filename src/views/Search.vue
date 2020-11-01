<template>
  <div :class="[{flexStart: step === 1}, 'wrapper']">
    <transition name="slide">
      <p class="logo" v-if="step === 1">Photonia</p>
    </transition>
    <transition name="fade">
      <MainImage v-if="step === 0"/>
    </transition>
    <Claim v-if="step === 0" />
    <SearchInput
      v-model="searchValue"
      @input="handleInput"
      :dark="step === 1"
      />
    <div class="results" v-if="results && !loading && step === 1">
      <Item v-for="item in results" :item="item" :key="item.id"/>
    </div>
  </div>
</template>

<script>
import debounce from 'lodash.debounce';
import Claim from '@/components/Claim.vue';
import SearchInput from '@/components/SearchInput.vue';
import MainImage from '@/components/MainImage.vue';
import Item from '@/components/Item.vue';

const API = 'https://pixabay.com/api/?key=18923603-d3c03a7301e1b80b95dd91273';

export default {
  name: 'Search',
  components: {
    Claim,
    SearchInput,
    MainImage,
    Item,
  },
  data() {
    return {
      loading: 'false',
      step: 0,
      searchValue: '',
      results: [],
    };
  },
  methods: {
    handleInput: debounce(function () {
      this.loading = true;
      console.log(this.searchValue);
      fetch(`${API}&q=${this.searchValue}&image_type=photo&per_page=100`)
        .then((response) => response.json())
        .then((data) => {
          this.results = data.hits;
          this.loading = false;
          this.step = 1;
        })
        .catch((error) => {
          console.log(error);
        });
    }, 500),
  },
};
</script>

<style lang="sass" scoped>
  .fade-enter, .fade-leave-active
    transition: opacity .3s ease

  .fade-enter, .fade-leave-to
    opacity: 0

  .slide-enter, .slide-leave-active
    transition: margin-top .7s ease

  .slide-enter, .slide-leave-to
    margin-top: -50px

  .wrapper
    position: relative
    display: flex
    flex-direction: column
    align-items: center
    justify-content: center
    width: 100%
    min-height: 100vh
    margin: 0
    padding: 50px 30px

  .flex-start
    justify-content: flex-start

  .logo
    position: absolute
    top: 40px
    font-weight: bold

</style>
