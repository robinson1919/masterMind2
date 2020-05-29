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
          :ref="casilla.sel4"
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
      selectedColor: Number,
      coderArr: Array
    },  
    data: () => ({
      cHint1: '',
      cHint2: '',
      cHint3: '',
      cHint4: '',
      selection: {},
      newArr: [],
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
        // verifica si hay alguna celda vacia
        
        for (let i = 0; i < this.newArr.length; i++) {
          var index = this.newArr[i].position;
          var cel = this.newArr[i].cel;
          if(this.casillas[index][cel] == this.coderArr[i]){
            console.log(this.coderArr[i]+'you won the game')
          }
          // console.log(this.casillas[index][cel])
          // console.log(this.coderArr[i])
          
          this.casillas.forEach(x => {
            this.coderArr.forEach(el => {
              if(x[cel] == el){
                console.log(x[cel])
              }
            });
          });
        }

        

        // for (let u = 0; u < this.coderArr.length; u++) {
          // console.log(this.coderArr[u])
          // for (let i = 0; i < this.casillas.length; i++) {
            // console.log(this.casillas[i][Object.keys(this.casillas[i])[u]])
            // if(this.coderArr[u] == this.casillas[i][Object.keys(this.casillas[i])[u]]){
            //   console.log(this.coderArr[u])
            // }
            
            // console.log(Object.keys(this.casillas[i])[u])
        //   }
        // }
        
        
            
            
          
            // if(this.casillas[i]['sel1'] == '' || this.casillas[i]['sel2'] == '' || this.casillas[i]['sel3'] == '' || this.casillas[i]['sel4'] == ''){
            //   return;
            // } else {
              
                // if(this.casillas[i]['sel1'] == this.coderArr[i] && this.casillas[i]['sel2'] == this.coderArr[i] && this.casillas[i]['sel3'] == this.coderArr[i] && this.casillas[i]['sel1'] == this.coderArr[i]){
                //   console.log('you won the game')
                // }
                
                
                // console.log(this.casillas[i][Object.keys(this.casillas[i])])
                
              



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
              );
            // }
            
            
          // console.log(this.casillas[i][Object.keys(this.casillas[i])[o]])
          // for (let o = 0; o < 4; o++) {
          // }
          
          
        
        
        

        // console.log(this.casillas.length)
      },

      selected(val, index){
        this.selection = { cel: val, position: index}
      },

      addColor(selectedColor){
        var index = "";
        var cel = "";
        index = this.selection.position;
        cel = this.selection.cel;
        if(index != undefined && cel != undefined){
          switch(selectedColor){
            case 1:
              this.casillas[index][cel] = 'blue';
              cel = '';
              index = '';
              break;

            case 2:
              this.casillas[index][cel] = 'red';
              this.selection = {};
              break;

            case 3:
              this.casillas[index][cel] = 'yellow';
              this.selection = {};
              break;

            case 4:
              this.casillas[index][cel] = 'green';
              this.selection = {};
              break;

            case 5:
              this.casillas[index][cel] = 'white';
              this.selection = {};
              break;

            case 6:
              this.casillas[index][cel] = 'black';
              this.selection = {};
              break;
          }
        }

        
      },
    },
    watch: {
      'selectedColor'(){
        // console.log(this.coderArr)
        if(this.selectedColor != 0){
          this.addColor(this.selectedColor);
        }
        
      },
      selection(){
        var ind = this.selection.position;
        var selec = this.selection.cel;
        // console.log(ind, selec)
        if(ind != undefined && selec != undefined){
          this.newArr.push(this.selection);
        }
        
        
       
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