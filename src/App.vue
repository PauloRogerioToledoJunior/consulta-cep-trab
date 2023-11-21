<template>
  
  <div>
    <div class="header">
      <ul>
        <li> <router-link to="/">Início</router-link> </li>
        <li> <router-link to="Via-Cep">Via Cep</router-link> </li>
        <li> <router-link to="About">Sobre</router-link> </li>
      </ul>
    </div>
    

    <router-view />

  </div>


</template>

<script setup>

</script>

<style scoped>
  *{
    margin: 0;
    padding: 0;
    font-family: sans-serif;
  }
  .header{
    padding: 24px 30px;
    display: flex;
    width: 100vw;
    background-color: #ccc;
  }

  .header ul{
    display: flex;
    list-style: none;
    gap: 40px;
  }

  .header ul a{
    text-decoration: none;
    color: black;
    font-weight: bold;
  }
</style>
