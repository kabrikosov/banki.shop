<template>
  <div id="search">
    <input type="text" id='search_input' placeholder="Поиск по названию картины" v-model="query" v-on:keyup.enter="onSearchClick">
    <button class="custom_button" type="submit" id="search_button" @click="onSearchClick">Найти</button>
  </div>
</template>

<script>
export default {
  name: "Search",
  props: {
    query: String,
  },
  data(){
    return {
      query: '',
    }
  },
  methods: {
    onSearchClick: function(){
      this.$emit('search', this.query)
      this.query = '';
    },
  }
}
</script>

<style scoped>

</style>
