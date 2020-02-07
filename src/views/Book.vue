<template>
  <div class="book">
    <!-- <h1>This is a Book page {{ $route.params.id }}</h1> -->
    <ApolloQuery :query="require('@/graphql/queries/Book.gql')" :variables="{ id: $route.params.id }">
       <template slot-scope="{ result: { data, loading }, isLoading }">
           <div v-if="isLoading">Loading...</div>
          <div v-else>
            <div>{{ data.book.title }}</div>
            <div>{{ data.book.author }}</div>
            <img :src="'http://localhost/graph/public/img/me.jpg'" alt="book cover">
            <div>
              <router-link :to="'/books/${data.book.id}/edit'" href="#" class="link-margin">Edit</router-link>
              <a href="#" class="link-margin">Delete</a>
            </div>
         </div>
       </template>
      </ApolloQuery>
  </div>
</template>


