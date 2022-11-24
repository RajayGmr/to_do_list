<template>
    <h1>Edit Project</h1>
  <form action="" >
    <label for="">Project Title</label>
    <input type="text" v-model="title">
    <label for="">Project Detail</label>
    <input type="text" v-model="detail">
    <button @click.prevent="EditProject">Edit Project</button>
  </form>
</template>

<script>
export default {
    props:['id'],
    data(){
        return{
            title:"",
            detail:"",
        }
    },  
    methods:{
        EditProject(){
            fetch('http://localhost:3000/projects/'+this.id,{
                method: "PATCH",
                headers:{
                    "Content-type":"application/json"
                },
                body:JSON.stringify({
                    title:this.title,
                    detail:this.detail
                })
            })
            .then(()=>{
                this.$router.push("/")
            })
            .catch((err)=>{
                console.log(error);
            })
        }
    },
    mounted(){
        fetch('http://localhost:3000/projects/'+this.id)
        .then((response)=>{
            return response.json()
        })
        .then((datas)=>{
            console.log(datas);
            this.title=datas.title;
            this.detail=datas.detail;
        })
        .catch((err)=>{
            console.log(err);
        })
    }

}
</script>

<style>

</style>