<template>
   <div class="project" @click="toggleProject">
       <div class="actions">
           <h3 @click="Redirect">{{project.title}}</h3>
           <img @click="deleteProject"  class="icons" src="https://image.flaticon.com/icons/png/512/542/542724.png" width="20">
       </div>
       <div  v-if="showDetails" class="details">
           <p>{{project.details}}</p>
        </div>
    </div>
   
   
</template>

<script>
export default {
    props:["project"],
    data(){
        return{
            showDetails:false,
        }
    },
    methods:{
        toggleProject(){
            this.showDetails = !this.showDetails;
        },
        deleteProject(){
            this.$emit("delete",this.project)
        },
        Redirect(){
          this.$router.push(`/edit/${this.project.id}`)

        }
    },
}


</script>

<style scoped>
  .project {
    margin: 20px auto;
    background: white;
    padding: 10px 20px;
    display: flex;
    
    border-radius: 4px;
    box-shadow: 1px 2px 3px rgba(0,0,0,0.05);
    border-left: 4px solid #e90074;

  }
  h3 {
    cursor: pointer;
  }
   .icons {
    font-size: 24px;
    margin-left: 10px;
    color: #bbb;
    cursor: pointer;
  }
  .details {
      padding:20px;
  }
  .actions {
    display: flex;
    justify-content: space-between;
    align-items: center;
  }
  .material-icons {
    font-size: 24px;
    margin-left: 10px;
    color: #bbb;
    cursor: pointer;
  }
  .material-icons:hover {
    color: #777;
  }
  /* completed projects */
  .project.complete {
    border-left: 4px solid #00ce89;
  }
  .project.complete .tick {
    color: #00ce89;
  }
</style>