<template>
  <v-container fluid>
    <Navigation>
      <Search v-on:search="search"/>
    </Navigation>
    <Content v-model:content="content" />
    <Navigation>
      <div id="contacts">
        <div id="contacts__container">
          <span id="phone">+7 (812) 555-55-55</span>
          <span id="address">г. Санкт-Петербург, ул. Ефимова, 3</span>
        </div>
      </div>
    </Navigation>
  </v-container>
</template>

<script>
import Navigation from "@/components/Navigation.vue";
import Search from "@/components/Search.vue";
import Content from "@/components/Content.vue";

export default {
  name: "MainPage",
  components: {Content, Search, Navigation},
  data(){
  return {
    searchQuery: '',
    }
  },
  methods: {
    search: function(args){
      this.searchQuery = args;
    },
  },
  computed: {
    content(){
      console.log(this.$store.state)
        return this.$data.searchQuery === ''
          ? this.$store.state
          : this.$store.state
            .filter(
              (el) =>
                el.name.includes(this.$data.searchQuery)
                || el.author.includes(this.$data.searchQuery)
            )
    }
  }
}
</script>

<style scoped lang="scss">
.navigation_container{
  margin-left: auto;
}

#phone::before{


}

</style>
