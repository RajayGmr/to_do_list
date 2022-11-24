<template>
  <nav class="main-nav">
    <router-link to="/">Projects</router-link> |
    <router-link :to="{name:'addProject'}">Add Projects</router-link>
  </nav>
</template>

<script>
export default {

}
</script>

<style>
.main-nav{
    text-align: center;
    margin: 40px auto;
}
.main-nav a{
    display: inline-block;
    text-decoration: none;
    margin: 0 10px;
    color: rgb(0, 0, 0);
    font-size: 18px;
}
a.router-link-active{
    border-bottom: 2px solid #00ce89;
    padding-bottom:4px ;
}
.main-nav a:hover{
    border-bottom: 2px solid rgb(255, 0, 128);
    color: rgb(255, 0, 128);
}

</style>