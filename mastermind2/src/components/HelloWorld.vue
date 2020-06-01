<template>
  <v-container>
    <v-row sm="12" md="12" class="mar" v-for="(casilla, index) in casillas" :key="index">

      <v-col sm="1" md="1">
        <v-text-field
          solo
          v-model="casilla.sel1"
          :class="[casilla.class1]"
          v-on:click="sendToP(true)"
          @click="selected('sel1', index, 'class1')"
        ></v-text-field>
      </v-col>

      <v-col sm="1" md="1">
         <v-text-field
          solo
          v-model="casilla.sel2"
          :class="[casilla.class2]"
          v-on:click="sendToP(true)"
          @click="selected('sel2', index, 'class2')"
        ></v-text-field>
      </v-col>

      <v-col sm="1" md="1">
         <v-text-field
          solo
          v-model="casilla.sel3"
          :class="[casilla.class3]"
          v-on:click="sendToP(true)"
          @click="selected('sel3', index, 'class3')"
        ></v-text-field>
      </v-col>

      <v-col sm="1" md="1" class="mr-5">
         <v-text-field
          solo
          v-model="casilla.sel4"
          :class="[casilla.class4]"
          v-on:click="sendToP(true)"
          @click="selected('sel4', index, 'class4')"
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
          :class="[casilla.hint1]"
        ></v-text-field>
      </v-col>
      <v-col sm="1" md="1">
        <v-text-field
          solo
          :class="[casilla.hint2]"
        ></v-text-field>
      </v-col>
      <v-col sm="1" md="1">
        <v-text-field
          solo
          :class="[casilla.hint3]"
        ></v-text-field>
      </v-col>
      <v-col sm="1" md="1">
        <v-text-field
          solo
          :class="[casilla.hint4]"
        ></v-text-field>
      </v-col>

      <!-- Button -->
      <v-col sm="1" md="1">
        <v-btn color="success" @click="CheckNadd(index)">          
          Set
        </v-btn>
      </v-col>
      <!-- Button -->
      <!-- hints end -->

      <!-- win modal start -->
      <v-dialog
        v-model="winModal"
        persistent :overlay="true"
        max-width="500px"
      >
        <v-card>
          <v-card-title
            class="headline grey lighten-2"
            primary-title
          >
            You won!
          </v-card-title>

          <v-card-text>
            Congratulations you won the game! click reset to start a new game.
          </v-card-text>

          <v-divider></v-divider>
          <v-card-actions>
            <v-spacer></v-spacer>
            <v-btn
              color="primary"
              text
              @click="cleanAll"
            >
              reset
            </v-btn>
          </v-card-actions>
        </v-card>
      </v-dialog>
      <!-- win modal end -->



    
      
     

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
      resVal: false,
      selection: {},
      newArr: [],
      oArr: [],
      matches: [],
      yellowMatch: [],
      code: false,
      winModal: false,
      igual: 0,
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
          class1: '',
          class2: '',
          class3: '',
          class4: '',
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

      CheckNadd(val){
        // verifica si hay alguna celda vacia
        var hintArr = [];
        var matchHint = [];
        var num = 0;

        for (let i = 0; i < this.newArr.length; i++) {
          var index = this.newArr[i].position;
          var cel = this.newArr[i].cel;
          // if(this.casillas[index][cel] == this.coderArr[i]){
          //   console.log(this.coderArr[i]+'you won the game')
          // }
          
          
          hintArr = [];
          this.casillas.forEach(x => {
            var codPosCel = x[cel];
            this.coderArr.forEach(el => {
              var derCo = el;
              if(codPosCel == derCo){

                // validate duplicated colors 
                this.oArr.push(codPosCel)                
                var sorted_arr = this.oArr.slice().sort();
                var results = [];
                for (var i = 0; i < sorted_arr.length - 1; i++) {
                    if (sorted_arr[i + 1] === sorted_arr[i]) {
                        results.push(sorted_arr[i]);
                    }
                }
                this.igual = results.length;
                // -------------------------------------------------
                
                if(Object.keys(x).indexOf(cel) == this.coderArr.indexOf(el)){
                  this.matches.push(Object.keys(x).indexOf(cel));
                  
                  this.casillas[val].hint1 = '';
                  this.casillas[val].hint2 = '';
                  this.casillas[val].hint3 = '';
                  this.casillas[val].hint4 = '';
                }

                if(Object.keys(x).indexOf(cel) != this.coderArr.indexOf(el)){
                  this.yellowMatch.push(Object.keys(x).indexOf(cel))
                }

              }
              el = '';
            });
            x[cel] = '';
            
          });
          cel = '';
          

        }

        this.oArr = [];
        
        
        // ----------------GOOD COLOR BAD POSITION-------------------------------
        switch(this.yellowMatch.length + this.matches.length - this.igual){
          case 1:
            this.casillas[val].hint1 = 'yellow';
            break;

          case 2:
            this.casillas[val].hint1 = 'yellow';
            this.casillas[val].hint2 = 'yellow';
            break;

          case 3:
            this.casillas[val].hint1 = 'yellow';
            this.casillas[val].hint2 = 'yellow';
            this.casillas[val].hint3 = 'yellow';
            break;

          case 4:
            this.casillas[val].hint1 = 'yellow';
            this.casillas[val].hint2 = 'yellow';
            this.casillas[val].hint3 = 'yellow';
            this.casillas[val].hint4 = 'yellow';
            break;
        }
        // ----------------GOOD COLOR BAD POSITION-------------------------------
        this.yellowMatch = [];
        this.igual = 0;



        // good color and position
        switch(this.matches.length){
          case 1:
            this.casillas[val].hint1 = 'black';
            break;

          case 2:
            this.casillas[val].hint1 = 'black';
            this.casillas[val].hint2 = 'black';
            break;

          case 3:
            this.casillas[val].hint1 = 'black';
            this.casillas[val].hint2 = 'black';
            this.casillas[val].hint3 = 'black';
            break;

          case 4:
            this.casillas[val].hint1 = 'black';
            this.casillas[val].hint2 = 'black';
            this.casillas[val].hint3 = 'black';
            this.casillas[val].hint4 = 'black';
            this.winModal = true;
            return;
            break;
        }
        // good color and position end

        this.matches = [];
        val = '';
        
        // Adds a new row 
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
            class1: '',
            class2: '',
            class3: '',
            class4: '',
          }
        );
      },

      selected(val, index, cls){
        this.selection = { cel: val, position: index, clas: cls}
      },

      addColor(selectedColor){
        var index = "";
        var cel = "";
        var classSel = "";
        index = this.selection.position;
        cel = this.selection.cel;
        classSel = this.selection.clas;
        if(index != undefined && cel != undefined){
          switch(selectedColor){
            case 1:
              this.casillas[index][classSel] = 'blue';
              this.casillas[index][cel]  = 'blue';
              cel = '';
              index = '';
              break;

            case 2:
              this.casillas[index][classSel] = 'red';
              this.casillas[index][cel] = 'red';
              this.selection = {};
              break;

            case 3:
              this.casillas[index][classSel] = 'yellow';
              this.casillas[index][cel] = 'yellow';
              this.selection = {};
              break;

            case 4:
              this.casillas[index][classSel] = 'green';
              this.casillas[index][cel] = 'green';
              this.selection = {};
              break;

            case 5:
              this.casillas[index][classSel] = 'white';
              this.casillas[index][cel] = 'white';
              this.selection = {};
              break;

            case 6:
              this.casillas[index][classSel] = 'black';
              this.casillas[index][cel] = 'black';
              this.selection = {};
              break;
          }
        }

        
      },

      cleanAll(){
        this.casillas.forEach(element => {
          this.resVal = true;
          this.$emit('resetCod', this.resVal);
          element.class1 = '';
          element.class2 = '';
          element.class3 = '';
          element.class4 = '';
          element.hint1 = '';
          element.hint2 = '';
          element.hint3 = '';
          element.hint4 = '';
          this.oArr = [];
          this.igual = 0;
          this.yellowMatch = [];
          this.matches = [];
          this.casillas = [
            {
              sel1: '',
              sel2: '',
              sel3: '',
              sel4: '',
              hint1: '',
              hint2: '',
              hint3: '',
              hint4: '',
              class1: '',
              class2: '',
              class3: '',
              class4: '',
            }
          ]
        });
        this.winModal = false;
      }
    },
    watch: {
      'selectedColor'(){
        if(this.selectedColor != 0){
          this.addColor(this.selectedColor);
        }
        
      },
      selection(){
        var ind = this.selection.position;
        var selec = this.selection.cel;
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