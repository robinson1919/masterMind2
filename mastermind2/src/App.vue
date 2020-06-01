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
              :class="[cod1]"
              @click="selectionCod('cod1')"
              v-on:click="dialog = true"
            ></v-text-field>
          </v-col>

          <v-col sm="1" md="1">
            <v-text-field
              solo
              :class="[cod2]"
              @click="selectionCod('cod2')"
              v-on:click="dialog = true"
            ></v-text-field>
          </v-col>

          <v-col sm="1" md="1">
            <v-text-field
              solo
              :class="[cod3]"
              @click="selectionCod('cod3')"
              v-on:click="dialog = true"
            ></v-text-field>
          </v-col>

          <v-col sm="1" md="1" class="mr-5">
            <v-text-field
              solo
              :class="[cod4]"
              @click="selectionCod('cod4')"
              v-on:click="dialog = true"
            ></v-text-field>
          </v-col>

          <v-col sm="1" md="1" class="mr-5">
            <v-btn color="success" @click="ready">Done</v-btn>
          </v-col>
        </v-row>

        <v-row cols="8" sm="6" md="3">
          <hello-world @modalStatus="modal" :selectedColor="color" :coderArr="codArr" @resetCod="resetAll"></hello-world>
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
            <!-- <button class="col-md-3 blue hv" @click="getColor(1)"></button> -->
            <input type="button" class="col-md-3 blue hv" @click="getColor(1)">
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
    color: 0,
    tic: '',
    cod1: '',
    cod2: '',
    cod3: '',
    cod4: '',
    selectedCod: '',
    codArr: [],
  }),

  methods: {

    modal(arg){
      this.dialog = arg;
    },

    resetAll(){
      this.cod1 = '';
      this.cod2 = '';
      this.cod3 = '';
      this.cod4 = '';
      this.codArr = [];
    },

    getColor(color){
      
      this.color = 0;
      this.color = color;
      
      if(this.color != 0){
        switch(this.color){
          case 1:

            switch(this.selectedCod){
              case 'cod1':
                this.cod1 = 'blue';
                this.selectedCod = '';
                break;

              case 'cod2':
                this.cod2 = 'blue';
                this.selectedCod = '';
                break;

              case 'cod3':
                this.cod3 = 'blue';
                this.selectedCod = '';
                break;

              case 'cod4':
                this.cod4 = 'blue';
                this.selectedCod = '';
                break;
            }
            break;

          case 2:
            switch(this.selectedCod){
              case 'cod1':
                this.cod1 = 'red';
                this.selectedCod = '';
                break;

              case 'cod2':
                this.cod2 = 'red';
                this.selectedCod = '';
                break;

              case 'cod3':
                this.cod3 = 'red';
                this.selectedCod = '';
                break;

              case 'cod4':
                this.cod4 = 'red';
                this.selectedCod = '';
                break;
            }
            break;

          case 3:
            switch(this.selectedCod){
              case 'cod1':
                this.cod1 = 'yellow';
                this.selectedCod = '';
                break;

              case 'cod2':
                this.cod2 = 'yellow';
                this.selectedCod = '';
                break;

              case 'cod3':
                this.cod3 = 'yellow';
                this.selectedCod = '';
                break;

              case 'cod4':
                this.cod4 = 'yellow';
                this.selectedCod = '';
                break;
            }
            break;
          
          case 4:

            switch(this.selectedCod){
              case 'cod1':
                this.cod1 = 'green';
                this.selectedCod = '';
                break;

              case 'cod2':
                this.cod2 = 'green';
                this.selectedCod = '';
                break;

              case 'cod3':
                this.cod3 = 'green';
                this.selectedCod = '';
                break;

              case 'cod4':
                this.cod4 = 'green';
                this.selectedCod = '';
                break;
            }
            break;

          case 5:

            switch(this.selectedCod){
              case 'cod1':
                this.cod1 = 'white';
                this.selectedCod = '';
                break;

              case 'cod2':
                this.cod2 = 'white';
                this.selectedCod = '';
                break;

              case 'cod3':
                this.cod3 = 'white';
                this.selectedCod = '';
                break;

              case 'cod4':
                this.cod4 = 'white';
                this.selectedCod = '';
                break;
            }
            break;

          case 6:

            switch(this.selectedCod){
              case 'cod1':
                this.cod1 = 'black';
                this.selectedCod = '';
                break;

              case 'cod2':
                this.cod2 = 'black';
                this.selectedCod = '';
                break;

              case 'cod3':
                this.cod3 = 'black';
                this.selectedCod = '';
                break;

              case 'cod4':
                this.cod4 = 'black';
                this.selectedCod = '';
                break;
            }
            break;
          }
      }
      
    },

    selectionCod(val){
      this.selectedCod = '';
      this.selectedCod = val;
    },

    ready(){
      if(this.codArr.length < 4){
        if(this.cod1 && this.cod2 && this.cod3 && this.cod4){
          this.codArr.push(this.cod1, this.cod2, this.cod3, this.cod4)
          console.log(this.codArr)
        }
      }    
      
    }
  },
  watch: {
    dialog(){
      this.color = 0;
      
    },
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