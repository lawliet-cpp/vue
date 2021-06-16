<template>
  <div class="home">
    <h1>Home Page</h1>
    <div v-if="projects.length">
      <div v-for="project in projects" :key="project.id">
        <SingleProject :project="project"  @delete="deleteProject" />

      </div>
  
     </div>
    
  </div>
</template>

<script>
import SingleProject from "../components/SignleProject.vue"
export default {
  name: 'Home',
  data(){
    return{
      projects:[],
    }
  },
  components:{SingleProject,},
  mounted(){
    fetch('http://127.0.0.1:3000/projects')
    .then(res=>res.json())
    .then(data=>this.projects = data)
    .catch(err=>console.log(err.message))
  },
  methods :{
    deleteProject(project){
      this.projects = this.projects.filter(item=>item.id!==project.id)
      fetch(`http://localhost:3000/projects/${project.id}`,{
        method:"DELETE",
        headers:{"Content-Type":"application/json"}
      })
      
    }
  }
}
</script>
