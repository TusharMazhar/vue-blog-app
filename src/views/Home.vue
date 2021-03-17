<template>
  <div class="home">
    
    <v-container>
      <div style="margin:10px 10px;">
        <router-link to="/create-blog" style="text-decoration:none"><v-btn color="pink white--text" > Create New Blog</v-btn></router-link>
      </div>
    </v-container>
     
    <v-container>
      <div style="margin-bottom:40px">
        <h1 style="text-align:center" v-if="blogs.length!=0">All Blogs</h1>
      </div>
      
      <v-row v-if="blogs.length>0">

        <div  v-for="blog in blogs" :key="blog.id" style="margin-left:20px;margin-bottom:15px" >
          <v-card
          class="mx-auto"
          width="350"
        >
          <span v-for="img in blog.images" :key="img.index">
            <img
              style="padding:0px 3px;margin-left:17px;margin-top:10px"
              v-if="img!='' && img!=null && img.length<2"
              class="white--text align-end"
              height="100px"
              width="150px"
              :src='img'
            />  
            <img
             v-for="i in img" :key="i.index"
              style="padding:0px 3px;margin-left:17px;margin-top:10px"
              v-else
              class="white--text align-end"
              height="100px"
              width="150px"
              :src='i'
            />          
          </span>
            <v-card-title style="color:green">{{blog.title}}</v-card-title>
            <v-card-text class="text--primary">
              <div>{{blog.description}}</div>
            </v-card-text>
          </v-card>
        </div>
        
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

}
</script>
