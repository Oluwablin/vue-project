<template>
    <div class="create">
        <h1>Edit Book</h1>
     <form action="#" method="POST" @submit.prevent="editBook">
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
              <button type="submit">Update Book</button>
          </div>
      </form>
    </div>
</template>

<!-- let us make some scripts here -->
<script>
import updateBook from '@/graphql/mutations/UpdateBook.gql'
import book from '@/graphql/queries/Book.gql'

export default {
    
    data() {
        return {
            title: '',
            author: '',
            image: '',
            description: '',
            link: '',
            featured: false,
            category_id: 1,
            book: null
            }
    },
    // Apollo-specific options
apollo: {
  // Advanced query with parameters
  // The 'variables' method is watched by vue
  book: {
    query: book,
    // Reactive parameters
    variables () {
      // Use vue reactive properties here
      if(this.$route && this.$route.params) {
      return {
        id: this.$route.params.id
      }
      }
    },
    
    // Optional result hook
    result ({ data, loading, networkStatus }) {
      this.title = data.book.title
      this.author = data.book.author
      this.image = data.book.image
      this.description = data.book.description
      this.link = data.book.link
      this.featured = data.book.featured
      this.category_id = data.category_id
    },
  },
},
    methods: {
        editBook() {
            // Call to the graphql mutation
    this.$apollo.mutate({
      // Query
      mutation: updateBook,
      // Parameters
      variables: {
        id: this.$route.params.id,
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
      this.$router.push('/books/${this.$route.params.id}')
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
