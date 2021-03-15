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

        <v-textarea v-model="description" outlined placeholder="Description" ref="field" :rules="descriptionRules" v-if="step===1">
        </v-textarea>

          <v-file-input
            v-model="images"
            v-if="step===2 && images.length>=0"
            label="File input"
            filled
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
              <v-list-item-avatar color="grey"></v-list-item-avatar>
              <v-list-item-content>
                <v-list-item-title class="headline">{{title}}</v-list-item-title>
              </v-list-item-content>
            </v-list-item>
        
            <v-img
              src="https://cdn.vuetifyjs.com/images/cards/mountain.jpg"
              height="194"
            ></v-img>
        
            <v-card-text>
               {{description}}
            </v-card-text>
        

      
        </v-card>




        <div style="text-align:center">
          <v-btn @click="prev"  class="mb-5" v-if="step>1 && step<=3" style="margin-right:10px">
            Prev
          </v-btn>
          <v-btn @click="next"  class="mb-5"  v-if="step<3">
            Next
          </v-btn>
     
          <v-btn @click="save"  class="mb-5" v-else>
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
        titleRules:[ v => v.length>0 || 'Min 1 Charcter'],
        descriptionRules: [v => v.length >100 || 'Min 100 characters'],
 
        images:[],
        title: '',
        description: '',
        snackbar: false,
        step:1,
        text: '',
        timeout: 5000
      }
  },
  methods:{
    next(){
      this.$refs.field.focus()
      if(this.$refs.field.validate()){
            this.step++
      }
       
    },
    save(){

      this.snackbar = true
      this.text = "Blog Saved Successfully"

      setTimeout(()=>{
        this.$router.push('/')
      },3000)
       
    },
    prev(){
       this.step--
    }
  }

}
</script>

