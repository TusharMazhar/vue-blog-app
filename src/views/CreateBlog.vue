<template>
  <div>
    <div style="margin-top:20px">
      <p style="text-align:center;font-size:25px;color:green;font-weight:bold"> Create New Blog </p>
    </div>
    <v-card class="mx-auto my-12" max-width="600">
      <v-snackbar v-model="snackbar" :timeout="timeout"  multi-line>
        {{ text }}
        <template v-slot:action="{ attrs }">
          <v-btn v-bind="attrs" @click="snackbar = false" color="success" text>
            Close
          </v-btn>
        </template>
      </v-snackbar>
      <div>
        <v-card-title class="justify-center" v-if="step<3">Step-{{step}} </v-card-title>
        <v-card-title class="justify-center" v-else style="font-size:25px;;color:red"> Preview  </v-card-title>
      </div>
      <div class="mx-6">
        <v-text-field
          v-if="step===1"
          v-model="title"
          outlined
          required
          ref="field"
          :rules="titleRules"
          placeholder="Title"
        ></v-text-field>
        <v-textarea 
          v-model="description" 
          outlined placeholder="Description" 
          ref="field" 
          :rules="descriptionRules" 
          v-if="step===1">
        </v-textarea>
        <v-file-input
          v-model="image1"
          v-if="step===2"
          label="Image Upload"
          filled
          multiple
          :rules="imageRules"
          ref="field"
          prepend-icon="mdi-camera"
          @change="onAddFiles"
        >
        </v-file-input> 
        <v-file-input
          v-model="image2"
          v-if="step===2 && image1.length>=1 "
          label="Image Upload"
          filled
          multiple
          :rules="imageRules"
          ref="field"
          @change="onAddFiles1"
          prepend-icon="mdi-camera"
        >
        </v-file-input> 
        <v-file-input
          v-model="image3"
          v-if="step===2 && image2.length>=1 "
          label="Image Upload"
          filled
          multiple
          @change="onAddFiles2"
          :rules="imageRules"
          ref="field"
          prepend-icon="mdi-camera"
        >
        </v-file-input> 
        <v-file-input
          v-model="image4"
          v-if="step===2 && image3.length>=1 "
          label="Image Upload"
          filled
          multiple
          @change="onAddFiles3"
          :rules="imageRules"
          ref="field"
          prepend-icon="mdi-camera"
        >
        </v-file-input>
        <v-file-input
          v-model="image5"
          v-if="step===2 && image4.length>=1 "
          label="Image Upload"
          filled
          multiple
          @change="onAddFiles4"
          :rules="imageRules"
          ref="field"
          prepend-icon="mdi-camera"
        >
        </v-file-input>
        <v-card
          flat
          v-if="step===3"
          max-width="344"
          class="mx-auto"
        > 
          <v-list-item>
            <v-list-item-content>
              <v-list-item-title class="headline" style="color:green">{{title}}</v-list-item-title>
            </v-list-item-content>
          </v-list-item>
          <img
            v-for="src in previews" :key="src.index"
            style="margin-left:10px"
            :src="src"
            height="100px"
            width="100px"
          />
          <img
            v-for="src in previews1" :key="src.index"
            style="margin-left:10px"
            :src="src"
            height="100px"
            width="100px"
          />
          <img
            v-for="src in previews2" :key="src.index"
            style="margin-left:10px"
            :src="src"
            height="100px"
            width="100px"
          />
          <img
            v-for="src in previews3" :key="src.index"
            style="margin-left:10px"
            :src="src"
            height="100px"
            width="100px"
          />
          <img
            v-for="src in previews4" :key="src.index"
            style="margin-left:10px"
            :src="src"
            height="100px"
            width="100px"
          />
          <v-card-text>
            {{description}}
          </v-card-text>
        </v-card>
        <div style="text-align:center">
          <v-btn @click="prev"  class="mb-5" v-if="step>1 && step<4" style="margin-right:10px">
            Prev
          </v-btn>
          <v-btn @click="next"  class="mb-5"  v-if="(step===1|| step===2) && image1.length===0 ">
            Next 
          </v-btn>
          <v-btn @click="next2"  class="mb-5"  v-else-if="step!=3">
            Next
          </v-btn>
          <v-btn @click="save"  class="mb-5" v-if="step===3">
            Save
          </v-btn>
        </div>
      </div>
    </v-card>
  </div>
</template>
<script>
export default {
  data() {
    return {
      previews: [],
      previews1: [],
      previews2: [],
      previews3: [],
      previews4: [],
      titleRules:[ v => v.length>0 || 'Min 1 Charcter'],
      descriptionRules: [v => v.length >100 || 'Min 100 characters'],
      imageRules:[() =>this.image1.length>0   || 'Minimum 1  or Maximum 5 image1 You will be able to select'],
      image1:[],
      image2:[],
      image3:[],
      image4:[],
      image5:[],
      images:[],
      uploadImage:null,
      title: '',
      description: '',
      snackbar: false,
      step:1,
      text: '',
      timeout: 5000,
    }
  },
  methods:{
    onAddFiles(files) {
    this.previews = [];
    files.forEach((file, index) => {
        const reader = new FileReader();
        reader.addEventListener('load', e => this.previews[index] = e.target.result);
        reader.readAsDataURL(file);
      })
    console.log('previews length',this.previews.length)
    },
    onAddFiles1(files) {
    this.previews1 = [];
    files.forEach((file, index) => {
        const reader = new FileReader();
        reader.addEventListener('load', e => this.previews1[index] = e.target.result);
        reader.readAsDataURL(file);
      })
    },
    onAddFiles2(files) {
    this.previews2 = [];
    files.forEach((file, index) => {
        const reader = new FileReader();
        reader.addEventListener('load', e => this.previews2[index] = e.target.result);
        reader.readAsDataURL(file);
      })
    },
    onAddFiles3(files) {
    this.previews3 = [];
    files.forEach((file, index) => {
        const reader = new FileReader();
        reader.addEventListener('load', e => this.previews3[index] = e.target.result);
        reader.readAsDataURL(file);
      })
    },
    onAddFiles4(files) {
    this.previews4 = [];
    files.forEach((file, index) => {
        const reader = new FileReader();
        reader.addEventListener('load', e => this.previews4[index] = e.target.result);
        reader.readAsDataURL(file);
      })
    },
    next(){
      this.$refs.field.focus()
      if(this.$refs.field.validate()){
        this.step++
      }        
    },
    next2(){
      this.step++
      console.log('preview',this.previews)
    },
    save(){

      console.log('image i arra',this.image1.length)
      
      this.images.push(this.previews,this.previews1,this.previews2,this.previews3,this.previews4)
      console.log('Vuex',this.images)
      this.$store.state.blogs.push({title:this.title,description:this.description,images:this.images})
      this.snackbar = true
      this.text = "Blog Saved Successfully"
      setTimeout(()=>{
        this.$router.push('/')
      },3000)
    },
    prev(){
      this.step--
    },
  }
}
</script>