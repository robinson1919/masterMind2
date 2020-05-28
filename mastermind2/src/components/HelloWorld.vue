<template>
  <v-container>
    <v-row sm="12" md="12" class="mar" v-for="(casilla, index) in casillas" :key="index">

      <v-col sm="1" md="1">
        <v-text-field
          solo
          v-model="casilla.sel1"
          :class="[casilla.sel1]"
          v-on:click="sendToP(true)"
          @click="selected('sel1', index)"
        ></v-text-field>
      </v-col>

      <v-col sm="1" md="1">
         <v-text-field
          solo
          v-model="casilla.sel2"
          :class="[casilla.sel2]"
          v-on:click="sendToP(true)"
          @click="selected('sel2', index)"
        ></v-text-field>
      </v-col>

      <v-col sm="1" md="1">
         <v-text-field
          solo
          v-model="casilla.sel3"
          :class="[casilla.sel3]"
          v-on:click="sendToP(true)"
          @click="selected('sel3', index)"
        ></v-text-field>
      </v-col>

      <v-col sm="1" md="1" class="mr-5">
         <v-text-field
          solo
          v-model="casilla.sel4"
          :class="[casilla.sel4]"
          v-on:click="sendToP(true)"
          @click="selected('sel4', index)"
        ></v-text-field>
      </v-col>

      <!--  -->
       <v-divider
          class="mx-4 divider"
          vertical
        ></v-divider>
      <!--  -->

      <!-- hints -->
      <v-col sm="1" md="1">
        <v-text-field
          solo
          :class="[cHint1]"
        ></v-text-field>
      </v-col>
      <v-col sm="1" md="1">
        <v-text-field
          solo
          :class="[cHint2]"
        ></v-text-field>
      </v-col>
      <v-col sm="1" md="1">
        <v-text-field
          solo
          :class="[cHint3]"
        ></v-text-field>
      </v-col>
      <v-col sm="1" md="1">
        <v-text-field
          solo
          :class="[cHint4]"
        ></v-text-field>
      </v-col>

      <!-- Button -->
      <v-col sm="1" md="1">
        <v-btn color="success" @click="CheckNadd">
          
          Set
        </v-btn>
      </v-col>
      <!-- Button -->
      {{selectedColor}}
      <!-- hints end -->



    
      
     

    </v-row>
  </v-container>
</template>

<script>
  export default {
    name: 'HelloWorld',  
    props: {
      selectedColor: {}
    },  
    data: () => ({
      cHint1: '',
      cHint2: '',
      cHint3: '',
      cHint4: '',
      selection: {},
      casillas: [
        {
          sel1: '',
          sel2: '',
          sel3: '',
          sel4: '',
          hint1: '',
          hint2: '',
          hint3: '',
          hint4: '',
        }
      ]
    }),
    created(){
      
    },

    

    methods: {
      sendToP(val){
        var dialog = val
        this.$emit('modalStatus', dialog);
      },

      CheckNadd(){
        this.casillas.push(
          {
            sel1: '',
            sel2: '',
            sel3: '',
            sel4: '',
            hint1: '',
            hint2: '',
            hint3: '',
            hint4: '',
          }
        )
      },
      selected(val, index){
        this.selection = { cel: val, position: index}
      },

      addColor(selectedColor){
        var index = "";
        var cel = "";
        index = this.selection.position;
        cel = this.selection.cel;

        switch(selectedColor){
          case 1:
            this.casillas[index][cel] = 'blue';
            break;

          case 2:
            this.casillas[index][cel] = 'red';
            break;

          case 3:
            this.casillas[index][cel] = 'yellow';
            break;

          case 4:
            this.casillas[index][cel] = 'green';
            break;

          case 5:
            this.casillas[index][cel] = 'white';
            break;

          case 6:
            this.casillas[index][cel] = 'black';
            break;
        }
      }
    },
    watch: {
      'selectedColor'(){
        this.addColor(this.selectedColor);
      }
    },

    
  }
</script>


<style scoped>

.divider {
  margin-right: 5rem;
  margin-left: 1rem;
}

.mar {
  margin-left: 1rem;
}

</style>