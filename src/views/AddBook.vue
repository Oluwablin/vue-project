<template>
    <div class="create">
        <h1>Create Book</h1>
     <form action="#" method="POST">
          <div class="form-group">
              <label for="title">Title</label>
              <input type="text" name="title" id="title">
          </div> 
          <div class="form-group">
              <label for="title">Author</label>
              <input type="text" name="author" id="author">
          </div>
          <div class="form-group">
              <label for="title">Image</label>
              <input type="text" name="image" id="image">
          </div>
          <div class="form-group">
              <label for="title">Description</label>
              <textarea name="description" id="description" cols="30" rows="10"></textarea>
          </div>
          <div class="form-group">
              <label for="title">Link</label>
              <input type="text" name="link" id="link">
          </div>
          <div class="form-group">
              <label for="title">Title</label>
              <input type="text" name="title" id="title">
          </div>
          <div class="form-group">
              <label><input type="checkbox" name="featured">Featured</label>
          </div>
         <div class="form-group">
             <select name="category" id="category" class="input-field input-normal">
             <option value="cat1">Category 1</option>
             <option value="cat2">Category 2</option>
             <option value="cat3">Category 3</option>
             </select>
          </div>
          <div class="form-group">
              <button type="submit">Add Book</button>
          </div>
      </form>
    </div>
</template>

// let us style our form here

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
