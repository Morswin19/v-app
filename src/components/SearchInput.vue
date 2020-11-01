<template>
      <input
        id="search"
        name="search"
        :value="value"
        :class="{ dark }"
        autocomplete="off"
        @input="handleChange"
      />
</template>

<script>
export default {
  name: 'SearchInput',
  props: {
    value: {
      type: String,
      required: true,
    },
    dark: {
      type: Boolean,
      default: false,
    },
  },
  methods: {
    handleChange(e) {
      this.$emit('input', e.target.value);
    },
  },
};
</script>

<style lang="sass" scoped>
        input
            height: 40px
            width: 250px
            border: none
            border-bottom: 2px solid white
            background: none
            outline: none
            color: white
            text-align: center
            font-size: 15px
            padding: 5px
            transition: box-shadow .3s
            // border-radius: 30px
        input:focus
            box-shadow: 0px 10px 20px -8px rgba(255,255,255,0.4)
            // background: rgba(0,0,0,0.5)
        .dark
            color: navy
            border-bottom-color: navy
        input:focus
            box-shadow: 0px 10px 20px -8px rgba(0,0,0,0.4)
            // background: rgba(0,0,0,0.5)
</style>
