<template>
  <div class="home">
       <v-container>

          <div style="margin:10px 10px;">
            <router-link to="/create-blog" style="text-decoration:none"><v-btn color="pink white--text" > Create New Blog</v-btn></router-link>
          </div>

       </v-container>
     
       <v-container>
          <div style="margin-bottom:10px">
                <h1 style="text-align:center" v-if="blogs.length!=0">All Blogs</h1>
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
              <div>{{blog.description}}</div>
            </v-card-text>
        
          </v-card>

            </v-col>
            
          </v-row> 
          <v-row v-else style="margin-top:10px">
            <div style="margin:auto">
                <p style="font-size:30px;font-weight:bold;color:red;text-align:center">No Blog Created</p>
            </div>
             
          </v-row> 
          
       </v-container>
  </div>
</template>

<script>


export default {
  name: 'Home',
  data(){
    return{
      blogs: this.$store.state.blogs
          
    }
  },
  created(){
   
  }
}
</script>
