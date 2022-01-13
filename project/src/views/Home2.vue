<template>
  <div>
    <v-row class="pa-3">
      <v-col cols="4">
        <!-- CARD FOR PLAYFAIR CIPHER -->
        <v-card flat  color="#E0F2F1" style="border:1px solid grey">
          <v-toolbar flat color="#004D40" dense dark>
            <v-toolbar-title >PLAYFAIR CIPHER</v-toolbar-title>
          </v-toolbar>
          <v-card-text>
            <v-col>
                <v-row >
                  <v-text-field solo @change="saveKeyword()" v-model="keyWord" outlined dense label="Keyword"/>
                </v-row>
              </v-col>
            
              <v-col>
                <v-row >
                  <v-text-field v-model="plainText" solo outlined dense label="Enter Plain Text"/>
                  <v-btn @click="encrypt()" icon class="mt-1 ml-2" color="#004D40">
                    <v-icon large>mdi-check</v-icon>
                  </v-btn>
                </v-row>
              </v-col>
              
            <span class="overline">
              Result: 
              <span class="font-weight-bold">{{result}}</span>
            </span>

            <v-divider></v-divider>
            <span>Key Square</span>
            <v-card color="#004D40">
              <center>
                <v-col sm="15" md="10" lg="9">
                  <v-row>
                    <template v-if="keyWord">
                      <v-sheet
                        v-for="(n,i) in arrKeyWords" 
                        :key="i"
                        color="white" 27
                        elevation="1"
                        class="ma-1"
                        height="50"
                        width="50"
                      >
                        <span class="font-weight-bold subtitle-1 ma-2">{{n}}</span>
                      </v-sheet>
                    </template>
                    <template v-else>
                      <v-sheet
                        v-for="(n,i) in 25" 
                        :key="i"
                        color="white"
                        elevation="1"
                        class="ma-1"
                        height="50"
                        width="50"
                      >
                        
                      </v-sheet>
                    </template>
                  </v-row>
                </v-col>
              </center>
              
            </v-card>
            

            
            
            
          </v-card-text>
        </v-card>
      </v-col>
      <v-col  cols="4">
        <!-- CARD FOR Homophonic Substitution CIPHER -->
        <v-card flat color="#ECEFF1" style="border:1px solid grey">
          <v-toolbar flat color="#263238" dense dark>
            <v-toolbar-title >Homophonic Substitution Cipher</v-toolbar-title>
          </v-toolbar>
          <v-card-text>
            <v-col>
                <v-row >
                  <v-text-field solo @change="homoEncrypt()" v-model="homoKeyWord" outlined dense label="Keyword"/>
                </v-row>
              </v-col>
            
              <v-col>
                <v-row >
                  <v-text-field v-model="homoPlainText" solo outlined dense label="Enter Plain Text"/>
                  <v-btn icon class="mt-1 ml-2" color="#263238">
                    <v-icon large>mdi-check</v-icon>
                  </v-btn>
                </v-row>
              </v-col>
              
            <span class="overline">
              Result: 
              <span class="font-weight-bold">{{homoResult}}</span>
            </span>

            <v-divider></v-divider>
            <span>Key Table</span>
            <v-card color="#263238" class="mt-2 pa-1">
              <template v-for="(n,i) in homoCipherText" >
                <v-chip outlined  color="#CFD8DC" :key="i" dense small class="ma-1">
                  <span :key="i"  >
                    {{Object.keys(n)[0]}}:
                    <!-- {{Object.values(n)[0].toString()}} -->
                    <span :key="i"  >
                    <!-- {{Object.keys(n)[0]}}: -->
                    {{Object.values(n)[0].toString()}}
                  </span>
                  </span>
                </v-chip>
              </template>
            </v-card>
          </v-card-text>
        </v-card>
      </v-col>
      <v-col  cols="4">
        <!-- CARD FOR DISRUPTED TRANSPOSITION CIPHER -->
        <v-card style="border:1px solid grey" color="#FFFDE7" flat>
          <v-toolbar flat color="#FFD600" dense dark>
            <v-toolbar-title >Disrupted Transposition</v-toolbar-title>
          </v-toolbar>
          <v-card-text>
            <v-col>
                <v-row >
                  <v-text-field v-model="disruptedKeyword" solo outlined dense label="Enter Plain Text"/>
                  <v-btn icon class="mt-1 ml-2" color="#FFD600" @click="saveDisruptedKeyword()">
                    <v-icon large>mdi-check</v-icon>
                  </v-btn>
                </v-row>
              </v-col>
              
            <span class="overline">
              Result: 
            </span>

            <v-divider></v-divider>
              <span v-if="disruptedResult" class="font-weight-bold title">{{disruptedResult}}</span>
              <span v-else class="font-weight-bold title">No Result</span>

          </v-card-text>
        </v-card>
      </v-col>
    </v-row>
    
  </div>
</template>

<script>
  export default {
    name: 'Home',
    components: {
    },
    data(){
      return{
        arrKeyWords: [],
        keyWord: '',
        plainText: '',
        result: 'No Result',
        letters:['A','B','C','D','E','F','G','H','I','K','L','M','N','O','P','Q','R','S','T','U','V','W','X','Y','Z'],
        homoCipherText: [
          {A: ['1','8']},
          {B: ['F']}, {C: ['R']}, {D: ['E']}, {E: ['S','H','T','O']}, 
          {F: ['M']}, {G: ['A']},{H: ['N']},{I: ['D','2']},{J: ['9']},{K: ['C']},{L: ['U']},
          {M: ['B']},{N: ['G','I']},{O: ['J','K']},{P: ['L']},{Q: ['P']},{R: ['Q']},{S: ['V','W']},
          {T: ['X','Y','Z']},{U: ['0']},{V: ['3']},{W: ['4']},{X: ['5']},{Y: ['6']},{Z: ['7']},
        ],
        homoKeyWord: '',
        homoPlainText: '',
        homoResult: 'No Result',
        ////------DISRUPTED KEYWORD--------////
        disruptedKeyword: '',
        disruptedResult: ''
      }
    },
    methods:{
      ////FUNCTION FOR DISRUPTED TRANSPOSITION////
      saveDisruptedKeyword(){
        this.disruptedResult = this.disruptedKeyword.toUpperCase().split('').sort(function(){
          return 0.5-Math.random()
        }).join('');
      },
      ////FUNCTION FOR HOMOPHONIC CIPHER//// - Not Yet Finished
      homoEncrypt(){
        console.log(this.homoKeyWord)
      },
     ////FUNCTION FOR PLAYFAIR//// - Not Yet finished
      saveKeyword(){
        this.arrKeyWords = this.keyWord.toUpperCase().split("")
        ////GENERATE 5x5 LETTER GRID////
        let tempLetters = this.letters.sort(() => Math.random() - 0.5)
        let  temp2 = new Set(this.arrKeyWords.concat(tempLetters))
        this.arrKeyWords = [...new Set(temp2)]
        console.log('TEMP',[...new Set(temp2)])
        

        ////If the plaintext contains J, then it is replaced by I. ////
        if(this.arrKeyWords.includes('J')){
          ////LOOP FOR CHANGING J INTO I////
          for(let i = 0; i < this.arrKeyWords.length; i++){
            if(this.arrKeyWords[i] == 'J'){
              this.arrKeyWords[i] = 'I'
            }
          }
          
        }else{
          console.log('NO J')
        }
        
        
        // console.log(this.arrKeyWords)
      }
    }
  }
</script>

<style >
.test{
  border: 1px solid red
}
</style>
