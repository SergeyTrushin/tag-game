<template>
  <div class="container">
    <NavBar />
    <Nuxt />
  </div>
</template>

<script>
  import NavBar from "@/components/NavBar"
  
  export default {
    components: {
      NavBar
    }
  }
</script>

<style lang="less">
  html {
    font-family:
    'Source Sans Pro',
    -apple-system,
    BlinkMacSystemFont,
    'Segoe UI',
    Roboto,
    'Helvetica Neue',
    Arial,
    sans-serif;
    font-size: 16px;
    word-spacing: 1px;
    -ms-text-size-adjust: 100%;
    -webkit-text-size-adjust: 100%;
    -moz-osx-font-smoothing: grayscale;
    -webkit-font-smoothing: antialiased;
    box-sizing: border-box;
    background: #f4f4f4;
  }

  *,
  *::before,
  *::after {
    box-sizing: border-box;
    margin: 0;
  }

  .container{
    width: 70%;
    max-width: 1200px;
    margin: 0 auto;
  }
</style>
