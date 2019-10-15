<template>
  <div class="question-box">
    <b-jumbotron>
    <template v-slot:lead>
      {{cau_hoi_khac.question}}
    </template>

    <hr class="my-4">
    <b-list-group>
      <b-list-group-item 
      v-for="(reps, index) in traloi " 
      :key="index"
      @click.prevent="selectedcauhoi(reps,index)"
      :class="[selectedItem === index ? 'selected':'']">{{reps}}</b-list-group-item>
    </b-list-group>

    <b-button variant="primary" href="#" 
    @click="submitAnswer()"
    :disabled="selectedItem===null">Submit</b-button>
    <b-button variant="success" href="#" @click="next_index()">Next</b-button>
    </b-jumbotron>
  </div>
</template>
<script>
export default {
  props: {
    //cauhoikhac biến trong prop đc truyền từ component cha là App
    cau_hoi_khac: Object,
    next_index: Function,
    increment: Function
  },
  data: function() {
    return {
      selectedItem: null,
      slectedValue: null,
    }
  },
  computed: {
    traloi () {
      let rep = [...this.cau_hoi_khac.incorrect_answers]
      rep.push(this.cau_hoi_khac.correct_answer)
      return rep
      
    }
  },
  methods:{
    selectedcauhoi(reps,index) {
      this.selectedItem = index;
      this.slectedValue = reps;
      console.log(reps)
    },
    submitAnswer() {
      //save câu tl có đúng k
      let isCorrect = false;
      if(this.slectedValue === this.cau_hoi_khac.correct_answer) {
        isCorrect = true
      }
      this.increment(isCorrect)
      console.log('this.selectedItem:'+' '+this.selectedItem)
      console.log('this.cau_hoi_khac.correct_answer:'+' '+this.cau_hoi_khac.correct_answer)
    },
  }
}
</script>
<style scoped>
  .list-group-item:hover {
    /* background-color: #eeeeee; */
    cursor: pointer;
  }
  .selected {
    background-color: coral;
  }
  .corect {
    background-color: chartreuse;
  }
  .incorect {
    background-color: cyan; 
  }
</style>