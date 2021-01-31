<template>
  <nav>
    <ul>
      <li><router-link to="/" exact>Game</router-link></li>
      <li><router-link to="/history" >History</router-link></li>
    </ul>
  </nav>
</template>

<script>
  export default {}
</script>

<style lang="less">
  nav{
    margin-top: 10px;
    ul{
      display: flex;
      list-style: none;
      padding: 0;
      li{
        margin-right: 15px;
        border: 1px solid;
        height: 30px;
        display: flex;
        justify-content: center;
        align-items: center;
        background: #ccc;
        padding: 10px;
        a{
          text-decoration: none;
          color:#000;
          opacity: .5;
          &.nuxt-link-active{
            color: blue;
            opacity: 1;
          }
        }
      }
    }
  }
</style>
