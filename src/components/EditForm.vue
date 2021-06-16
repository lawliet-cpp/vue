<template>
  <form @submit.prevent="handleSubmit">
    <label>Title</label>
    <input type="text"  required v-model="title"  />
    <label>Details</label>
    <input type="text" required v-model="details" />

    <button type="submit">Update</button>
  </form>
</template>


<script>
import axios from "axios"
export default {
  data() {
    return {
      title:"",
      details: "",
    };
  },
  mounted() {

    
    axios.get(`http://localhost:3000/projects/${this.$route.params.id}`)
    .then(data=>{
        console.log(data)
        this.title = data.data.title
        this.details = data.data.details
    })
    .catch(err=>{
        console.log(err.message)
    })
  },
  methods:{
    
    handleSubmit(){
      const project = {
        title:this.title,
        details:this.details,
        completed:false,
      }
      fetch(`http://localhost:3000/projects/${this.$route.params.id}`,{
        method:"PATCH",
        headers:{"Content-Type":"application/json"},
        body:JSON.stringify(project)
      }).then(()=>{
          this.$router.push("/")
      })
    }
  }
};
</script>


<style>
form {
  max-width: 420px;
  margin: 30px auto;
  background: white;
  text-align: left;
  padding: 40px;
  border-radius: 10px;

}
label {
  color: #aaa;
  display: inline-block;
  margin: 25px 0 15px;
  font-size: 0.6em;
  text-transform: uppercase;
  letter-spacing: 1px;
  font-weight: bold;
}
input,
select {
  display: block;
  padding: 10px 6px;
  width: 100%;
  box-sizing: border-box;
  border: none;
  border-bottom: 1px solid #ddd;
  color: #555;
}
input[type="checkbox"] {
  display: inline-block;
  width: 16px;
  margin: 0 10px 0 0;
  position: relative;
  top: 2px;
}
button{
  width:100px;
  height:30px;
  margin:20px;
  background:#42b883;
  border: none;
  border-radius:10px;
  font-weight: bold;
  color:white;
  

}
.pill {
  display: inline-block;
  margin: 20px 10px 0 0;
  padding: 6px 12px;
  background: #eee;
  border-radius: 20px;
  font-size: 12px;
  letter-spacing: 1px;
  font-weight: bold;
  color: #777;
  cursor: pointer;
}
</style>

