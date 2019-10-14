<template>
  <div class="question-box">
    <b-jumbotron>
    <template v-slot:lead>
      {{cau_hoi_khac.question}}
    </template>

    <hr class="my-4">
    <b-list-group>
      <b-list-group-item 
      v-for="(reps, index) in traloi" 
      :key="index"
      @click.prevent="selectedcauhoi(index)"
      :class="[selectedItem === index ? 'selected':'']">{{reps}}</b-list-group-item>
    </b-list-group>

    <b-button variant="primary" href="#">Submit</b-button>
    <b-button variant="success" href="#" @click="next_index()">Next</b-button>
    </b-jumbotron>
  </div>
</template>
<script>
export default {
  props: {
    //cauhoikhac biến trong prop đc truyền từ component cha là App
    cau_hoi_khac: Object,
    next_index: Function
  },
  data: function() {
    return {
      selectedItem: null,
      //active: 'selected'
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
    selectedcauhoi(index) {
      this.selectedItem = index;
      console.log(index)
    }
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