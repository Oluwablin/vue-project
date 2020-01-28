<template>
  <div class="home">

    <!-- Apollo Query for Category-->

   <ApolloQuery :query="require('../graphql/queries/Categories.gql')">
     <template slot-scope="{ result: { data, loading } , isLoading}">
      <div v-if="isLoading">Loading...</div>
        <div v-else>
         <a href="#" v-for="category of data.categories" :key="category.id" @click="selectCategory(category.id)" class="link-margin">
          {{ category.id }}. {{ category.name }}
         </a>
       </div>
     </template>
   </ApolloQuery><br>

    <!-- Apollo Query for Books -->

   <ApolloQuery :query="require('../graphql/queries/Category.gql')" :variables= "{id: selectedCategory}">
     <template slot-scope="{ result: { data, loading } , isLoading}">
       <div v-if="isLoading">Loading...</div>
       <div v-else>
         <div v-for="book of data.category.books" :key="book.id">
           {{ book.id }}. {{ book.title }} <br> {{ book.author }}<br> {{ book.description }}
         </div>
       </div>
     </template>
   </ApolloQuery>
  </div>
</template>

<script>
// @ is an alias to /src
import gql from 'graphql-tag'

export default {
  name: 'home',                                                                                                                                                                                      
  components: {
    
  },
  data() {
    return {
      selectedCategory: 2,
categories: ''
    }
  },
  apollo: {
   // Simple query that will update the vue property
  categories: gql`{
    categories {
    id
    name
  }
  }`,
  },
  //variable for click
  methods: {
    selectCategory(category){
      this.selectedCategory = category
    }
  }
}
</script>

<style>
  .link-margin 
 {
   margin-right :24px; 
 }
</style>