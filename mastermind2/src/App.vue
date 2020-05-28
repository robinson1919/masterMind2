<template>
  <v-app id="inspire">
    <v-container grid-list-xs>
      <v-card>
        <v-card-title ml-5 primary-title class="headline">
          MasterMind
        </v-card-title>

        <v-row cols="12" sm="4" md="4" class="mar">
          <v-col sm="1" md="1">
            <v-text-field
              solo
              v-on:click="dialog = true"
            ></v-text-field>
          </v-col>

          <v-col sm="1" md="1">
            <v-text-field
              solo
              v-on:click="dialog = true"
            ></v-text-field>
          </v-col>

          <v-col sm="1" md="1">
            <v-text-field
              solo
              v-on:click="dialog = true"
            ></v-text-field>
          </v-col>

          <v-col sm="1" md="1" class="mr-5">
            <v-text-field
              solo
              v-on:click="dialog = true"
            ></v-text-field>
          </v-col>
        </v-row>

        <v-row cols="8" sm="6" md="3">
          <hello-world @modalStatus="modal" :selectedColor="color"></hello-world>
        </v-row>
      </v-card>

      <!-- modal start -->
      
      <v-dialog
        v-model="dialog"
        width="350"
      >
        <v-card>
          <v-card-title
            class="headline grey lighten-2"
            primary-title
          >
            Pick a color
          </v-card-title>

          <v-row class="col-md-12 mx-auto">
            <input type="text" class="col-md-3 blue hv" @click="getColor(1)">
            <input type="text" class="col-md-3 red hv" @click="getColor(2)">
            <input type="text" class="col-md-3 yellow hv" @click="getColor(3)">
          </v-row>
          <v-row class="col-md-12 mx-auto">
            <input type="text" class="col-md-3 green hv" @click="getColor(4)">
            <input type="text" class="col-md-3 white hv" @click="getColor(5)">
            <input type="text" class="col-md-3 black hv" @click="getColor(6)">
          </v-row>

          <v-divider></v-divider>
          <v-card-actions>
            <v-spacer></v-spacer>
            <v-btn
              color="primary"
              text
              @click="dialog = false"
            >
              accept
            </v-btn>
          </v-card-actions>
        </v-card>
      </v-dialog>
      <!-- modal end -->
    
    
    </v-container>
  </v-app>  
</template>

<script>
import HelloWorld from './components/HelloWorld';

export default {
  name: 'App',

  components: {
    HelloWorld,
  },

  data: () => ({
    dialog: false,
    color: '',
  }),

  methods: {

    modal(arg){
      this.dialog = arg;
    },

    getColor(color){
      this.color = color;
    }
  },
};
</script>


<style  scoped>

.mar {
  margin-left: 1rem;
}

.blue {
  background-color: blue;
}

.red {
  background-color: red;
}

.white {
  background-color: white;
}

.yellow {
  background-color: yellow;
}

.green {
  background-color: green;
}

.black {
  background-color: black;
}

.hv {
  cursor: pointer;
}

</style>