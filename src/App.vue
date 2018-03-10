<template>
  <div id="app">
      <Slide></Slide>
  </div>
</template>
<script>
  import Slide from './component/Slide'
export default {
  name: 'app',
  components:{
    Slide
  }
}
</script>
<style>
  *{
    margin:0;
    padding:0;
    border: 0;
    outline: 0;
    font-weight: normal;
    font-style: normal;
    font-size: 100%;
    font-family: inherit;
    vertical-align: baseline
  }
  input[type=search]::-webkit-search-cancel-button,
  input[type=search]::-webkit-search-decoration {
    -webkit-appearance: none;
  }
  html,
  body {
    -webkit-overflow-scrolling: touch;
    height: 100%;
    overflow-x: hidden;
    box-sizing: border-box;
  }

  body {
    line-height: 2;
  }

</style>
