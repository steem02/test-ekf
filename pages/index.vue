<template lang=pug>
  div
    .search.container-fluid
      .center.row
        input.field.col-3(type="text" placeholder='Поиск' v-model="searchString")
    .container-fluid
      item(:prop="filteredArticles")
</template>

<script>
import item from '~/components/item.vue'
export default {
  data() {
    return { 
      message: '', 
      searchString: '',
      articles: []
    }
  },
  mounted() {
      const ip = this.$axios.$get('https://swapi.co/api/people').then((resource) => {this.articles.push(resource);console.dir(this.articles)});
      // console.log(ip.url);
    
  },
  computed: {
      // Вычисленное свойство, которое содержит только те статьи, которые соответствуют searchString.
      filteredArticles: function () {
          let articles_array = this.articles,
              searchString = this.searchString;

          if(!searchString){
              return articles_array;
          }

          searchString = searchString.trim().toLowerCase();

          articles_array = articles_array.filter(function(item){
              if(item.title.toLowerCase().indexOf(searchString) !== -1){
                  return item;
              }
          })

          // Возвращает массив с отфильтрованными данными.
          return articles_array;
      }
  },
  components: {
    item
  }
}
</script>

<style lang=sass>
  .center
    justify-content: center
  .search
    padding-top: 100px
    padding-bottom: 30px
  .field
    min-width: 300px
    min-height: 50px
    border: 2px solid #bae1e2
    box-shadow: 1px 1px 20px #bae1e2
    &:focus
      border: none
      outline: none

</style>

