<template>
  <div class="wrapper">
    <div class="search">
      <label for="search">Search: </label>
      <input
        id="search"
        name="search"
        v-model="searchValue"
        @input="handleInput"
      />
    </div>
    <ul class="results">
      <li v-for="item in results" :key="item.id">
        <p>{{item.tags}}</p>
      </li>
    </ul>
  </div>
</template>

<script>
import debounce from 'lodash.debounce';

const API = 'https://pixabay.com/api/?key=18923603-d3c03a7301e1b80b95dd91273';

export default {
  name: 'Search',
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
    width: 100%
    margin: 0
    padding: 30px
    .search
      display: flex
      flex-direction: column
      width: 250px
      label
        font-family: 'Trebuchet MS', 'Lucida Sans Unicode', 'Lucida Grande', sans-serif
      input
        height: 20px
        width: 100%
        border: none
        border-bottom: 2px solid blue
</style>
