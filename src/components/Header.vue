<template>
  <div>
    <b-nav tabs>
      <b-nav-item disabled>Fanci quiz app</b-nav-item>
      <b-nav-item disabled>counter: {{cau_tl_dung}}/{{tong_answer}}</b-nav-item>
    </b-nav>
  </div>
</template>
<script>
export default {
  props: [
    'tong_answer',
    'cau_tl_dung'
  ]
    
  
}
</script>