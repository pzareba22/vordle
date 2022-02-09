<template>
  <div class="main">
    <header class="mainHeader">
      <h1>Vordle</h1>
    </header>
    <div class="lettergrid"></div>
    <div class="keyboard">
      <div class="keybaordRow"></div>
      <div class="keybaordRow"></div>
      <div class="keybaordRow"></div>
    </div>

  </div>
</template>

<script>
  export default {
    
  }
</script>

<style  scoped>
*{
    font-family: sans-serif;
    box-sizing: border-box;
    margin: 0;
    padding: 0;
}

.main {
    width: 45vw;
    height: 100vh;
    margin: 0 auto;
    background-color: #f6f6f6;
    display: flex;
    flex-direction: column;
}

.mainHeader {
    background-color: #BFEE9B;
    color: #fff;
    padding: 2rem 0;
    text-align: center;
    font-size: x-large;
}


</style>