<template>
  <div class="home">
    <h1>Home</h1>
    <Nav @filterValue="current=$event" :curr="current"></Nav>
    <div v-for="project in filteredProjects" :key="project.id">
      <SingleProject :proj="project" @delete="deletelist" @updatelist="Updatelist"></SingleProject>
    </div>
    
  </div>
</template>

<script>

import Nav from '../components/Nav'
import SingleProject from '../components/SingleProject'
// @ is an alias to /src

export default {
  data(){
    return{
      projects:[],
      current:"all",
    }
  },
  methods:{
    deletelist(id){
      this.projects=this.projects.filter(project=>{
        return project.id!=id;
      })
    },
    Updatelist(id){
      let findProject=this.projects.find(project=>{
          return project.id===id;
      });
      findProject.complete=!findProject.complete

    }
  },
  components: {
    Nav,
    SingleProject,
    
  },
  mounted(){
    fetch('http://localhost:3000/projects')
    .then((response)=>{
      // console.log(response);
      return response.json()
    })
    .then((datas)=>{
      // console.log(datas);
      this.projects=datas;
    })
    .catch(()=>{

    })
  },
  computed:{
    filteredProjects(){
      if(this.current==="complete"){
        return this.projects.filter((project)=>{
          return project.complete;
        })
      }
      else if(this.current==="ongoing"){
        return this.projects.filter((project)=>{
          return !project.complete;
        })

      }
      else{
        return this.projects;
      }
    }
  }
}
</script>
