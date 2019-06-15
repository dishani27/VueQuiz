<template>
  <div id="navbar">
    <b-nav >
      <b-nav-item disabled> Quiz App </b-nav-item>
      <b-nav-item disabled>Question Number: {{currentNum}} / 10 </b-nav-item>
   </b-nav>
  </div>
</template>

<script>
export default {
  props: [
    // 'totalNum',
    'correctNum',
    'currentNum'
  ]
}
</script>

<style scoped>
#navbar{
  background-color: rgba(148,71,31,1);
  padding-top: 2%;
  padding-bottom: 1.1%;
  margin-bottom: 1.6%;
  color: white;
}
a.nav-link.disabled {
  color: white;
  font-weight: 600;
}
.nav{
  padding-left: 38%;
}
@media (max-width:1200px){
    .nav {
    padding-left: 35%;
    }
}
@media (max-width:992px){
    .nav {
    padding-left: 34%;
    }
}
@media (max-width:768px){
    .nav {
    padding-left: 30%;
    }
}
@media (max-width:640px){
    .nav {
    padding-left: 20%;
    }
}@media (max-width:480px){
    .nav {
    padding-left: 7%;
    }
}@media (max-width:360px){
    .nav {
    padding-left: 0%;
        margin: 0% -2%;
    }
}
</style>

