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
      <Item
        v-for="item in results"
        :item="item"
        :key="item.id"
        @click.native="handleModalOpen(item)"/>
    </div>
    <div class="lds-dual-ring" v-if="step === 1 && loading"></div>
    <Modal
      v-if="modalOpen"
      @closeModal="modalOpen = false"
      :item="modalItem"
    />
    <img src='./assets/pixaLogo.png' class="pixaLogo" />
  </div>
</template>

<script>
import debounce from 'lodash.debounce';
import Claim from '@/components/Claim.vue';
import SearchInput from '@/components/SearchInput.vue';
import MainImage from '@/components/MainImage.vue';
import Item from '@/components/Item.vue';
import Modal from '@/components/Modal.vue';

const API = 'https://pixabay.com/api/?key=18923603-d3c03a7301e1b80b95dd91273';

export default {
  name: 'Search',
  components: {
    Claim,
    SearchInput,
    MainImage,
    Item,
    Modal,
  },
  data() {
    return {
      modalOpen: false,
      modalItem: null,
      loading: 'false',
      step: 0,
      searchValue: '',
      results: [],
    };
  },
  methods: {
    handleModalOpen(item) {
      this.modalOpen = true;
      this.modalItem = item;
    },
    handleInput: debounce(function () {
      this.loading = true;
      fetch(`${API}&q=${this.searchValue}&image_type=photo&per_page=120`)
        .then((response) => response.json())
        .then((data) => {
          this.results = data.hits;
          this.loading = false;
          this.step = 1;
          // console.log(data.hits[0]);
        })
        .catch((error) => {
          console.log(error);
        });
    }, 500),
  },
};
</script>

<style lang="sass" scoped>
  @import url('https://fonts.googleapis.com/css2?family=Montserrat:wght@300;400;500;600;900&display=swap')
  *
    box-sizing: border-box
    margin: 0
    padding: 0
    -webkit-font-smoothing: antialiased
    -moz-osx-font-smoothing: grayscale

  body
    font-family: 'Montserrat', sans-serif
    font-weight: 500

  .headWrapper
    position: fixed

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
    left: 50px
    font-weight: bold
    margin-bottom: 50px

  .results
    display: flex
    flex-wrap: wrap
    justify-content: center
    margin-top: 50px
    grid-gap: 20px

  .pixaLogo
    position: absolute
    width: 50px
    height: 50px
    bottom: 20px
    right: 20px

  .lds-dual-ring
    margin-top: 100px
    display: inline-block
    width: 80px
    height: 80px

  .lds-dual-ring:after
    content: " "
    display: block
    width: 64px
    height: 64px
    margin: 8px
    border-radius: 50%
    border: 6px solid black
    border-color: black transparent black transparent
    animation: lds-dual-ring 1.2s linear infinite

  @keyframes lds-dual-ring
    0%
      transform: rotate(0deg)

    100%
      transform: rotate(360deg)

</style>
