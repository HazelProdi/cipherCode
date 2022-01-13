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
              <!-- UI HERE -->
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
            <!-- UI HERE -->
          </v-card-text>
        </v-card>
      </v-col>
      <v-col  cols="4">
        <!-- CARD FOR DISRUPTED TRANSPOSITION CIPHER -->
        <v-card style="border:1px solid grey" color="#FFFDE7" flat>
          <v-toolbar flat color="#FFD600" dense dark>
            <v-toolbar-title >Disrupted Transposition</v-toolbar-title>
          </v-toolbar>
          <v-card>
            <tr v-for="(item, i) in rowData" :key="i" >
              <th scope="row">{{ item.mail }}</th>
              <td>{{ item.date }}</td>
              <td>{{ item.adress }}</td>
              <td>{{ item.company }}</td>
              <td>{{ item.fliers }}</td>
            </tr>
          </v-card>
          <!-- <v-card-text>
            <v-card color="#004D40">
              <center>
                <v-col cols="12">
                  <v-row>
                    <template v-if="dtKeyword">
                      <v-sheet
                        v-for="(n,i) in dtKeyword.length" 
                        :key="i"
                        color="white"
                        elevation="1"
                        class="ma-1"
                        height="25"
                        width="25"
                      >
                        <span class="font-weight-bold subtitle-1 ma-2">{{n}}</span>
                      </v-sheet>
                      
                    </template>
                    
                  </v-row>
                </v-col>

                <v-col cols="12">
                  <v-row >
                    <v-sheet
                      v-for="(n,i) in dtKeyword" 
                      :key="i"
                      color="white"
                      elevation="1"
                      class="ma-1"
                      height="25"
                      width="25"
                    >
                      <span class="font-weight-bold subtitle-1 ma-2">{{n}}</span>
                    </v-sheet>
                  </v-row>
                </v-col>

                <v-col cols="12">
                  <v-row>
                    <span  v-for="(n,i) in dtKeyword.length" :key="i">
                      <v-sheet
                        
                        v-for="(nn, ii) in dtPlainText"
                        :key="ii"
                        color="white"
                        elevation="1"
                        class="ma-1"
                        height="25"
                        width="25"
                      >
                        <span  class="font-weight-bold subtitle-1 ma-2">{{nn}}</span>
                      </v-sheet>
                    </span>
                    
                  </v-row>
                </v-col>

              </center>
              
            </v-card> 
          </v-card-text> -->
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
        arr: [],
        newArr: [],
        dtSequence: [],
        dtKeyword: 'birthday',
        dtPlainText: 'We confirm the delivery of the documents later',
        //---------
        mail:'',
    date:'',
    adress:'',
    company:'',
    fliers:'',
    rowData:[] //the declared array
      }
    },
    methods:{
      addItem(){
        var my_object = {
          mail:this.mail,
          date:this.date,
          adress:this.adress,
          company: this.company,
          fliers: this.fliers
        };
        this.rowData.push(my_object)

        this.mail = '';
        this.date = '';
        this.adress = '';
        this.company = '';
        this.fliers = '';
      },
      get(){
    //     for (let i = 0; i < this.keyWord.length; i++) {
    //         this.createCell(row.insertCell(i), i, 'row');
    //       }
      },
      createCell(){

      },
      getRowa1(){
        // console.log('FROM getRowa1', this.arr)
        for(let i = 0;i < this.dtPlainText.length; i++){
          this.dtPlainText.split('')
           for (let index = 0; index < this.arr.length; index++) {
            //  const element = this.arr[index];
              this.arr[index].chars = []

            if(this.arr[index] == this.dtPlainText[i]){
              this.arr[index].chars.push(this.dtPlainText[i])

            }else{
              console.log('test')
              // this.arr[index - 1].chars = []
              // this.arr[index - 1].chars.push(this.dtPlainText[i])
            }
             
           }
          console.log(this.arr, 'FROM getRowa1')


          // this.arr.map(r => {
          //   r.chars = []
          //   r.chars.push(this.dtPlainText[i])
          //   return r
          // })

        }

      },
      async getRow1(){
        let newPlainText = this.dtPlainText.toUpperCase().replace(/\s/g, '*')
        // let arr1 = []
        for(let i = 0; i < this.dtKeyword.length; i++){
          let a = {}
          a.key = this.dtKeyword[i]
          this.arr.push(a)
          a = {}
        }

        console.log(this.arr,'aaaaaaaaaaaa')
        console.log(newPlainText, 'newPlainText')
        



        
        
        
        


          

        
        

      },
      async getRow2(){
        let rowCount = this.dtKeyword.toUpperCase().split('').length
        let keyWord = this.dtKeyword.toUpperCase().split('')
        let shuffledIndex = keyWord.map(value => ({value, sort: Math.random()}))
                .sort((a, b) => a.sort - b.sort)
                .map(({ value }) => value)
        // let plainText = this.dtPlainText.toUpperCase().split('')
        for(let i = 0; i < keyWord.length; i++){
          // var obj = {
          //   [keyWord[i]]: {chars: [], seq: shuffledIndex.indexOf(keyWord[i])}
          // }
          var obj = {
            key: keyWord[i], chars: [], seq: shuffledIndex.indexOf(keyWord[i])
          }
          this.newArr.push(obj)
          obj = {}

            

          
        }


        

        console.log(rowCount, 'rowCount')
        console.log(keyWord, 'keyWord')
        console.log(this.newArr, 'newArr')


      },
      ///==============///
        getRow(){
            let temp = {}
            let arr = this.dtKeyword.toUpperCase().split('')  
            let shuffledIndex = arr.map(value => ({value, sort: Math.random()}))
                .sort((a, b) => a.sort - b.sort)
                .map(({ value }) => value)
            for(let i = 0; i < arr.length; i++){

                temp.seq = shuffledIndex.indexOf(arr[i])
                temp.keyValue = arr[i]
                temp.arrText = []
                this.dtSequence.push(temp)
                temp = {}
            }


            // console.log(this.dtSequence.map(s => s.seq),'SEQ')
            // console.log(this.dtSequence.map(kv => kv),'KeyValue')
        },
        getValues(){
          let tempText = this.dtPlainText.replace(/\s/g, '*').toUpperCase().split('') 
          // console.log(tempText)
          for(let i = 0; i<tempText.length; i++){
            for(let ii = 0; ii < this.dtSequence.length; ii++){
              if(i == ii){
                this.dtSequence.map(r => {
                  r.arrText.push(tempText[i])
                  return r
                })
              }
            }
            // console.log( this.dtSequence, 'HEREEEEEEEEEEE')
          }
        },
        get1(){
            // let temp = {}
            // let arr = this.dtKeyword.toUpperCase().split('')
            // let shuffledIndex = arr.map(value => ({value, sort: Math.random()}))
            //     .sort((a, b) => a.sort - b.sort)
            //     .map(({ value }) => value)
            // for(let i = 0; i < arr.length; i++){
            //     temp.seq = shuffledIndex.indexOf(arr[i])
            //     temp.keyValue = arr[i]
            //     temp.arrText = []
            //     this.dtSequence.push(temp)
            //     temp = {}
            // }

            // console.log(this.dtSequence.map(s => s.seq),'SEQ')
            // console.log(this.dtSequence.map(kv => kv.keyValue),'KeyValue')

        },
        // get2(){
        //     console.log('test')

        // }
    },
    async created(){
      this.addItem()
         this.getRow1()
         await this.getRowa1()

         this.getRow2()
      
         this.getRow()
         this.getValues()
          // await this.getText()
        await this.get1()
        // await this.get2()

    }
  }
</script>

<style >
.test{
  border: 1px solid red
}
</style>
