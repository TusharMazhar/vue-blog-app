<template>
  <div>
    <div style="margin-top:20px">
       <p style="text-align:center;font-size:25px;color:green;font-weight:bold"> Create New Blog </p>
    </div>
    <v-card class="mx-auto my-12" max-width="600">
      <v-snackbar v-model="snackbar" :timeout="timeout">
        {{ text }}

        <template v-slot:action="{ attrs }">
          <v-btn v-bind="attrs" @click="snackbar = false" color="success" text>
            Close
          </v-btn>
        </template>
      </v-snackbar>

      <div>
        <v-card-title class="justify-center">Step-{{step}} </v-card-title>
      </div>
      <div class="mx-6">
        <v-text-field
          v-if="step===1"
          v-model="title"
          outlined
          placeholder="Title"
        ></v-text-field>

        <v-textarea v-model="description" outlined placeholder="Description" v-if="step===1">
        </v-textarea>
        <v-file-input
          v-if="step===2"
          label="File input"
          multiple
          filled
          prepend-icon="mdi-camera"
        >
        </v-file-input>  

        <div style="text-align:center">
          <v-btn @click="next" :loading="isLoading" class="mb-5">
            Next
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
        title: '',
        description: '',
        isDomain: false,
        isLoading: false,
        snackbar: false,
        step:1,
        text: '',
        timeout: 5000
      }
  },
  methods:{
    next(){
       this.step++
    }
  }

}
</script>

