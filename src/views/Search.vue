<template>
  <div class="wrapper">
    <Claim />
    <SearchInput />
    <ul class="results">
      <li v-for="item in results" :key="item.id">
        <p>{{item.tags}}</p>
      </li>
    </ul>
  </div>
</template>

<script>
import debounce from 'lodash.debounce';
import Claim from '@/components/Claim.vue';
import SearchInput from '@/components/SearchInput.vue';

const API = 'https://pixabay.com/api/?key=18923603-d3c03a7301e1b80b95dd91273';

export default {
  name: 'Search',
  components: {
    Claim,
    SearchInput,
  },
  data() {
    return {
      searchValue: '',
      results: [],
    };
  },
  methods: {
    handleInput: debounce(function () {
      fetch(`${API}&q=${this.searchValue}&image_type=photo&per_page=100`)
        .then((response) => response.json())
        .then((data) => {
          this.results = data.hits;
        })
        .catch((error) => {
          console.log(error);
        });
    }, 1000),
  },
};
</script>

<style lang="sass" scoped>
  .wrapper
    display: flex
    flex-direction: column
    align-items: center
    justify-content: center
    width: 100%
    height: 100vh
    margin: 0
    padding: 50px 30px
    background-image: url('../assets/background3.jpg')
    background-repeat: no-repeat
    background-size: cover
    background-position: 50% 0%

</style>
