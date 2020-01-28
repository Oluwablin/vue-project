<template>
  <div class="home">
    <!-- Apollo Query for Category-->
  <ApolloQuery :query="require('@/graphql/queries/Categories.gql')">
    <!-- The result will automatically updated -->
    <template slot-scope="{ result: { data, loading } , isLoading}">
      <!-- Some content -->
      <div v-if="isLoading">Loading...</div>
      <div v-else>
        <a href="#" v-for="category of data.categories" :key="category.id" class="category">
          {{ category.id }}. {{ category.name }}
        </a>
      </div>
    </template>
  </ApolloQuery>
    <!-- Apollo Query for Books -->
  <ApolloQuery :query="require('@/graphql/queries/Books.gql')">
    <!-- The result will automatically updated -->
    <template slot-scope="{ result: { data, loading } , isloading}">
      <!-- Some content -->
      <div v-if="isloading">Loading...</div>
      <div v-else>
        <div v-for="book of data.books" :key="book.id">
          {{ book.id }}. {{ book.title }}
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
categories: ''
    }
  },
  apollo: {
  // Simple query that will update the 'hello' vue property
  categories: gql`{
    categories {
    id
    name
  }
  }`,
  },
}
</script>
<style>
.link-margin {
 margin-right :24px; 
}
</style>