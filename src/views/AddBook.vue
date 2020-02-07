<template>
    <div class="create">
        <h1>Create Book</h1>
     <form action="#" method="POST" @submit.prevent="addBook">
          <div class="form-group">
              <label for="title">Title</label>
              <input type="text" name="title" id="title" v-model="title">
          </div> 
          <div class="form-group">
              <label for="title">Author</label>
              <input type="text" name="author" id="author" v-model="author">
          </div>
          <div class="form-group">
              <label for="title">Image</label>
              <input type="text" name="image" id="image" v-model="image">
          </div>
          <div class="form-group">
              <label for="title">Description</label>
              <textarea name="description" id="description" cols="30" rows="10" v-model="description"></textarea>
          </div>
          <div class="form-group">
              <label for="title">Link</label>
              <input type="text" name="link" id="link" v-model="link">
          </div>
          <div class="form-group">
              <label><input type="checkbox" name="featured" v-model="featured">Featured</label>
          </div>
         <div class="form-group">
             <!-- <select name="category" id="category" class="input-field input-normal">
             <option value="cat1">Category 1</option>
             <option value="cat2">Category 2</option>
             <option value="cat3">Category 3</option>
             </select> -->
             <ApolloQuery :query="require('@/graphql/queries/Categories.gql')">
               <template slot-scope="{ result: { data, loading } , isLoading }">
                 <div v-if="isLoading">Loading...</div>
                    <select v-else v-model="category">
                       <option v-for="category of data.categories" :key="category.id" value="category.id">
                          {{ category.name }}
                       </option>
                   </select>
                </template>
             </ApolloQuery>
          </div>

          <div class="form-group">
              <button type="submit">Add Book</button>
          </div>
      </form>
    </div>
</template>

<!-- let us make some scripts here -->
<script>
import addBook from '@/graphql/mutations/CreateBook.gql'

export default {
    
    data() {
        return {
            title: '',
            author: '',
            image: '',
            description: '',
            link: '',
            featured: false,
            category_id: 1
            }
    },
    methods: {
        addBook() {
            // Call to the graphql mutation
    this.$apollo.mutate({
      // Query
      mutation: addBook,
      // Parameters
      variables: {
        title: this.title,
        author: this.author,
        image: this.image,
        link: this.link,
        description: this.description,
        featured: this.featured,
        category_id: this.category_id
      }
    }).then((data) => {
      console.log(data)
      this.$router.push('/')
    }).catch((error) => {
      console.error(error)
    })
            // alert('adding new book')
        }
    }
}
</script>

<!-- let us style our form here -->

<style scoped>
   .form-group {
       margin-bottom: 32px;
   }
   input[type="text"]{
       padding: 10px 14px;
   }
   button {
       padding: 15px;
       background-color: #0278ff;
       color: white;
       border-radius: 3px;
       font-size: 16px;
   }

</style>
