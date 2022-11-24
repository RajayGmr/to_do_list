<template>
  <div class="filter-nav">
    <button @click="filterBy('all')" :class="{active:curr==='all'}">All</button>
    <button @click="filterBy('complete')" :class="{active:curr==='complete'}">Complete</button>
    <button @click="filterBy('ongoing')" :class="{active:curr==='ongoing'}">Ongoing</button>
  </div>
</template>

<script>
export default {
    props:['curr'],
    methods:{
        filterBy(value){
            //alert(value)
            this.$emit("filterValue",value)
        }
    }

}
</script>

<style>
.filter-nav button{
    background: none;
    border:none;
    color: rgb(91, 59, 0);
    outline: none;
    font-size: 12px;
    text-transform: uppercase;
    margin-right: 12px;
    font-weight: bold;
    cursor: pointer;
}
.filter-nav button:hover{
    text-decoration:2px solid underline;  
}
button.active{
    color: black;
    text-decoration: 2px solid underline rgb(24, 203, 24);
}

</style>