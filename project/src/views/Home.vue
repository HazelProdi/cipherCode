<template>
  <div>
    <v-row class="pa-3">
      <v-col cols="3">
        <!-- CARD FOR PLAYFAIR CIPHER -->
        <v-card flat  color="#E0F2F1" style="border:1px solid grey">
          <v-toolbar flat color="#004D40" dense dark>
            <v-toolbar-title >PLAYFAIR CIPHER</v-toolbar-title>
          </v-toolbar>
              <!-- UI HERE -->
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
      <v-col  cols="5">
        <!-- CARD FOR Homophonic Substitution CIPHER -->
        <v-card flat color="#ECEFF1" style="border:1px solid grey">
          <v-toolbar flat color="#263238" dense dark>
            <v-toolbar-title >Homophonic Substitution Cipher</v-toolbar-title>
          </v-toolbar>
          <v-card-text>
            <!-- UI HERE -->
            <v-card>
              <v-card-text>
                  <v-row no-gutters>
                    <v-col cols="10">
                      <small class="red--text" v-if="checkNumber()">Numeric Characters is not allowed.</small> 
                      <v-text-field  @change="checkNumber()" v-model="hs_PlainText" outlined dense label="Enter Plain Text"/>
                    </v-col>
                    <v-col cols="2">
                      <v-btn :disabled="checkNumber() || !hs_PlainText" large icon color="primary" @click="hs_encrypt(hs_PlainText)">
                        <v-icon>
                          mdi-check
                        </v-icon>
                      </v-btn>
                    </v-col>
                    <v-col>
                      <span class="title">Result: {{hs_result}}</span>
                    </v-col>
                  </v-row>
                  <v-divider></v-divider>
                  <span class="title">Hint:</span>
                  <v-row no-gutters> 

                      <span v-for="(k, i) in hs_letters" :key="i" class="ml-3">
                        <v-col >
                          <span class="title red--text">{{k.letter}}</span>
                        <span class="title" v-if="k.cipherText != ' '"> = {{k.cipherText.toString()}}</span>
                        </v-col>
                        
                      </span>
                    
                    
                  </v-row>
              </v-card-text>
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
            <small v-if="checkForDuplicate" class="red--text">Keyword has Duplicate Characters.</small>
            <v-text-field v-model="dtKeyword" outlined dense label="Enter Keyword"/>
            <v-row no-gutters>
              <v-col cols="10"> 
                <v-text-field :disabled="checkForDuplicate || !dtKeyword" @change="checkForDuplicate()" v-model="dtPlainText" outlined dense label="Enter Plain Text"/>
              </v-col>
              <v-col cols="2">
                <v-btn :disabled="checkForDuplicate" large icon color="primary" @click="dt_encrypt()">
                  <v-icon>
                    mdi-check
                  </v-icon>
                </v-btn>
              </v-col>
              <v-col>
                <span class="title">Result: </span>
                  <span class="title">{{dtResult.toUpperCase()}}</span>
              </v-col>
            </v-row>
            <v-card color="#F9A825">
              <v-card-text >
                <!-- <center> -->
                  <span class="subtitle-2">Sequence</span>
                  <v-col cols="12">
                  <v-row>
                    <v-sheet
                      v-for="(v,i) in dtKeyword"
                      :key="i"
                      color="white"
                      elevation="1"
                      height="25"
                      width="25"
                      class="ml-2"
                    >
                      <span>{{i}}</span>
                    </v-sheet>
                  </v-row>
                </v-col>
                <span class="subtitle-2">Keyword</span>
                <v-col cols="12">
                  <v-row>
                    <v-sheet
                      v-for="(v,i) in dtKeyword"
                      :key="i"
                      color="white"
                      elevation="1"
                      height="25"
                      width="25"
                      class="ml-2"
                    >
                      <span>{{v.toUpperCase()}}</span>
                    </v-sheet>
                  </v-row>
                </v-col>
                <span class="subtitle-2">Plain Text</span>
                <v-col>
                  <v-row>
                    <span v-for="(v,i) in groupedValues" :key="i">
                      <v-sheet
                        v-for="(vv,ii) in v.map(r => r.value.toUpperCase())" :key="ii"
                        color="white"
                        elevation="1"
                        height="25"
                        width="25"
                        class="ml-2 mb-2"
                      > 
                        <span>{{vv.toUpperCase()}}</span>
                      </v-sheet>
                    </span>
                  </v-row>
                </v-col>
              </v-card-text>
            </v-card> 
          </v-card-text>
        </v-card>
      </v-col>
    </v-row>
    
  </div>
</template>


<script>
import _ from 'lodash'
  export default {
    name: 'Home',
    components: {
    },
    data(){
      return{
        // DISRUPTED TRANSPOSITION VARIABLES //
        groupedValues: [],
        arr: [],
        dtSequence: [],
        dtKeyword: '',
        dtPlainText: '',
        dtResult: '',
        // HOMOPHONIC SUBSTITUTION VARIABLES //
        hs_result: '',
        hs_PlainText: '',
        hs_letters: [
          {letter: "A", cipherText: ["D","9"]},
          {letter: "B", cipherText: ["X"]},
          {letter: "C", cipherText: ["S"]},
          {letter: "D", cipherText: ["F"]},
          {letter: "E", cipherText: ["Z","7","2","1"]},
          {letter: "F", cipherText: ["E"]},
          {letter: "G", cipherText: ["H"]},
          {letter: "H", cipherText: ["C"]},
          {letter: "I", cipherText: ["V","3"]},
          {letter: "J", cipherText: ["I"]},
          {letter: "K", cipherText: ["T"]},
          {letter: "L", cipherText: ["P"]},
          {letter: "M", cipherText: ["G"]},
          {letter: "N", cipherText: ["A","5"]},
          {letter: "O", cipherText: ["Q","0"]},
          {letter: "P", cipherText: ["L"]},
          {letter: "Q", cipherText: ["K"]},
          {letter: "R", cipherText: ["J"]},
          {letter: "S", cipherText: ["R","4"]},
          {letter: "T", cipherText: ["U","6"]},
          {letter: "U", cipherText: ["O"]},
          {letter: "V", cipherText: ["W"]},
          {letter: "W", cipherText: ["M"]},
          {letter: "X", cipherText: ["Y"]},
          {letter: "Y", cipherText: ["B"]},
          {letter: "Z", cipherText: ["N"]},
          {letter: " ", cipherText: [" "]},

        ],
        // PLAYFAIR CIPHER VARIABLES //
        pf_plainText: 'Hjello Wojrld'
       
      }
    },
    computed: {
      // DISRUPTED TRANSPOSITION COMPUTED FUNCTIONS //
      checkForDuplicate(){
        let toFindDuplicates = this.dtKeyword.split('').filter((item, index) => this.dtKeyword.indexOf(item) !== index)
        if(toFindDuplicates.length != 0){
          return true
        }else{
          return false
        }
      },
      // HOMOPHONIC SUBSTITUTION COMPUTED FUNCTIONS //
      
    },
    methods:{
      // DISRUPTED TRANSPOSITION FUNCTIONS //
      dt_encrypt(){
        let plainText = this.dtPlainText.toUpperCase().replace(/\s/g, '*').split('') // CONVERT PLAIN TEXT TO UPPERCASE THEN REPLACE WHITE SPACES INTO ASTERIK (*) //
        var i,j, temporary, chunk = this.dtKeyword.length;
        // LOOP TO SEPARATE THE PLAINTEXT INTO CHUNK //
        for (i = 0,j = plainText.length; i < j; i += chunk) {
          temporary = plainText.slice(i, i + chunk);
          this.dt_assignRows(temporary) // CALL THE dt_assignRows METHOD //
        } 
      },
      dt_assignRows(data){
        // LOOP FOR ASSIGNING VALUES USING KEYWORD {value: "", key:"", seq:""} //
        for(let i = 0 ; i < this.dtKeyword.length; i++){
          let a = {}
          a.value = data[i]
          a.key = this.dtKeyword[i]
          let shuffledIndex = this.dtKeyword.split('').map(value => ({value, sort: Math.random()}))
            .sort((a, b) => a.sort - b.sort)
            .map(({ value }) => value)
          a.seq = shuffledIndex.indexOf(this.dtKeyword.split('')[i])
          this.arr.push(a)
          a={}
        }
        this.arr = this.arr.filter(r => {return r.key && r.value}) // FILTER RECORDS WITH KEY AND VALUE //
        this.groupedValues = _.mapValues(_.groupBy(this.arr, 'key'),
          clist => clist.map(key => _.omit(key, 'keys')));
        const objectArray = Object.entries(this.groupedValues);
          let b = []

        objectArray.forEach(([key, value]) => {
          console.log(key)
          let q = value.map(r => {
            return r.value
          }).toString()
          b.push(q.toString().toUpperCase())
          q = {}
        });
        this.dtResult = b.toString().split(',').toString().replace(',', '').toUpperCase()
        
      },
      // HOMOPHONIC SUBSTITUTION FUNCTIONS //
      checkNumber(){
        let a = this.hs_PlainText.split('')
        console.log(a)
        for(let j =0; j < a.length; j++){
          let b = typeof a[j]
          if(b == 'Number' || a.includes('0') || a.includes('1') || a.includes('2')|| a.includes('3') || a.includes('4')
            || a.includes('5') || a.includes('6')|| a.includes('7') || a.includes('8')|| a.includes('9') || a.includes('10')){
            return true
          }else{
            return false
          }
        }
      },
      hs_encrypt(data){
        console.log(data)
        let tempText = this.hs_PlainText.toUpperCase().split('')
        let tempArr = []
        for(let i = 0; i < tempText.length; i++){
          let a = this.hs_letters.filter(r => r.letter == tempText[i]).map(r => r.cipherText)[0]
          if(this.hs_letters.map(r => r.letter).includes(tempText[i])){
            if(a.length > 1){
              var item = a[Math.floor(Math.random()*a.length)];
              tempArr.push(item)
            }else{
              tempArr.push(a.toString())
            }
          }
          this.hs_result = tempArr.toString().replace(/,/g, '')
          console.log('HEREEE',this.hs_result)

        }
      },
      // PLAYFAIR FUNCTIONS //
      pf_decrypt(){
        let arrKeyWords = this.pf_plainText.toUpperCase().replace(' ','*').split("")
        ////If the plaintext contains J, then it is replaced by I. ////
        if(arrKeyWords.includes('J')){
          ////LOOP FOR CHANGING J INTO I////
          for(let i = 0; i < arrKeyWords.length; i++){
            if(arrKeyWords[i] == 'J'){
              arrKeyWords[i] = 'I'
            }
          }
          console.log('arrKeyWords', arrKeyWords)
          
        }else{
          console.log('NO J')
        }



        // this.arrKeyWords = this.keyWord.toUpperCase().split("")
        // ////GENERATE 5x5 LETTER GRID////
        // let tempLetters = this.letters.sort(() => Math.random() - 0.5)
        // let  temp2 = new Set(this.arrKeyWords.concat(tempLetters))
        // this.arrKeyWords = [...new Set(temp2)]
        // console.log('TEMP',[...new Set(temp2)])
        

        // ////If the plaintext contains J, then it is replaced by I. ////
        // if(this.arrKeyWords.includes('J')){
        //   ////LOOP FOR CHANGING J INTO I////
        //   for(let i = 0; i < this.arrKeyWords.length; i++){
        //     if(this.arrKeyWords[i] == 'J'){
        //       this.arrKeyWords[i] = 'I'
        //     }
        //   }
          
        // }else{
        //   console.log('NO J')
        // }
        
        
        // console.log(this.arrKeyWords)
      }
    },
    created(){
      this.pf_decrypt()
    }
  }
</script>

<style >
.test{
  border: 1px solid red
}
</style>
