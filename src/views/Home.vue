<template>
  <div class="home">

       <div>
         <router-link to="/create-blog">Create Blog</router-link>
       </div>
       <v-container>
          <div >
                <h1 style="text-align:center">All Blogs</h1>
          </div>
          
          <v-row v-if="blogs.length>0">

            <v-col  v-for="blog in blogs" :key="blog.id">
            <v-card
            class="mx-auto"
            max-width="200"
          >
            <v-img
              class="white--text align-end"
              height="200px"
              src="https://cdn.vuetifyjs.com/images/cards/docks.jpg"
            >
              <v-card-title>{{blog.title}}</v-card-title>
            </v-img>
        
            <v-card-text class="text--primary">
              <div>{{blog.des}}</div>
            </v-card-text>
        
          </v-card>

            </v-col>
            
          </v-row> 
          <v-row v-else>
             <p>No Blog created</p>
          </v-row> 
          
       </v-container>
  </div>
</template>

<script>


export default {
  name: 'Home',
  data(){
    return{
      blogs:[
        {id:1,title:'python 3',des:'asdfgdfghfhgfjfjgj'},
        {id:2,title:'python 3',des:'asdfgdfghfhgfjfjgj'},
        {id:3,title:'python 3',des:'asdfgdfghfhgfjfjgj'},
        {id:4,title:'python 3',des:'asdfgdfghfhgfjfjgj'},
        {id:5,title:'python 3',des:'asdfgdfghfhgfjfjgj'},
        {id:6,title:'python 3',des:'asdfgdfghfhgfjfjgj'},

      ]
    }
  }
}
</script>
