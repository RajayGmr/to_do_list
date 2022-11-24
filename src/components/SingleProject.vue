<template>
    <div class="project" :class="{complete:proj.complete}">
        <div class="container">
            <div>
                <h2 @click.self="showDetail=!showDetail">{{proj.title}}</h2>     
            </div>
            <div>
                <i class="fas fa-trash-alt" @click="DeleteList"></i>
                <router-link :to="{name:'editProject',params:{id:proj.id}}"><i class="far fa-edit" ></i></router-link>
                <i class="fas fa-check" @click="completeproject"></i>
            </div>
            
        </div> 
        <div v-if="showDetail">
            <p>{{proj.detail}}</p>        
        </div>
        {{proj.complete}} 
        
    </div>
      
</template>

<script>
export default {
    props:['proj'],
    data(){
        return{
            showDetail:false,
            api:'http://localhost:3000/projects'
        }
    },
    methods:{
        DeleteList(){
            // alert("hi")
            fetch(this.api+"/"+this.proj.id,{method:"DELETE"})
            .then(()=>{
                this.$emit('delete',this.proj.id)
            })
            .catch((error)=>{
                console.log(error);
            })
        },
        completeproject(){
            let updateCompleteroute=this.api+'/'+this.proj.id;
            //console.log(updateCompleteroute);
            fetch(updateCompleteroute,{
                method:"PATCH",
                headers:{
                    "Content-Type":"application/json"
                },
                body:JSON.stringify(
                    {
                        complete:!this.proj.complete
                    }
                )
            })
            .then(()=>{
                this.$emit('updatelist',this.proj.id)
            })
            .catch((error)=>{
                console.log(error)
            })

        }
    }

}
</script>

<style>
.project{
    padding: 20px;
    background-color: bisque;
    
    margin: 10px;
    border-radius: 15px;

    border-left: 10px solid red;
}
h2{
    color: rgb(11, 11, 243);
    cursor: pointer;
}
.container{
    display: flex;
    justify-content: space-between;
    align-items: center;
}
.far{
    margin-left: 20px;
    margin-right: 20px;
}
.fa-trash-alt:hover{
    cursor: pointer;
    color: red;
    text-shadow: 0 0 10px red;
}
.fa-edit:hover{
    cursor: pointer;
    color: orange;
    text-shadow: 0 0 10px orange;
}
.fa-check:hover{
    cursor: pointer;
    color: green;
    text-shadow: 0 0 10px green;
}
.complete{
    border-left-color: green;
}

</style>