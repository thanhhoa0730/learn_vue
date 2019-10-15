<template>
  <div id="app">
    <Header
      :cau_tl_dung="cautldung"
      :tong_answer="tonganswer">
      
    </Header>
    <b-container class="bv-example-row">
      <b-row>
        <b-col sm="6" offset="3">
          <question-box
            v-if="cauhoi.length"
            :cau_hoi_khac="cauhoi[index]"
            :next_index="nextItem"
            :increment="incrementApp"
          >
          </question-box>
        </b-col>
      </b-row>
    </b-container>
    
  </div>
</template>

<script>
import Header from './components/Header'
import QuestionBox from './components/QuestionBox'
export default {
  name: 'app',
  components: {
    Header,
    QuestionBox
  },
  data() {
    return {
      cauhoi: [],
      index: 0,
      cautldung: 0,
      tonganswer: 0
    }
  },
  methods:
  {
    nextItem() {
      this.index++
    },
    incrementApp(isCorrect) {
      if(isCorrect) {
        this.cautldung++
      }
      this.tonganswer++
    }
  },
  mounted: function() {
    fetch('https://opentdb.com/api.php?amount=10&category=27&type=multiple', {
      method:'get'
    })
    //lấy data
    .then((response)=>{
      return response.json()
    })
    .then((jsondt)=> {
      this.cauhoi = jsondt.results
    })
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
