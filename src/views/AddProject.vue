<template>
  <form @submit.prevent="handleSubmit">
    <label>Title: </label>
    <input type="text" v-model="title" required>
    <label>Details: </label>
    <textarea v-model="details" required></textarea>
    <button>Add Project</button>
  </form>
</template>

<script>
export default {
  data() {
    return {
      title: '',
      details:''
    }
  },
  methods:{
    handleSubmit(){
      let project = {
        title: this.title,
        details: this.details,
        complete: false,
      }
      fetch('http://localhost:3000/projects/', {
        method:'POST',
        headers: {"Content-Type": "application/json"},
        body: JSON.stringify(project),
      }).then(()=>this.$rooter.push("/"))
      .catch((err)=>console.log(err));
    }
  }

}
</script>

<style>
form{
  background: #fff;
  padding: 20px;
  border-radius: 10px;
}
label{
  display: block;
  color: #bbb;
  text-transform: uppercase;
  font-size: 14px;
  font-weight: bold;
  letter-spacing: 1px;
  margin: 20px 0 10px 0;
}
input{
  padding: 10px;
  border: 0;
  box-shadow: rgba(0, 0, 0, 0.24) 0px 3px 8px;
  width: 100%;
  box-sizing: border-box;
  }
  textarea{
    padding: 10px;
    box-shadow: rgba(0, 0, 0, 0.24) 0px 3px 8px;
    border: 0;
    width: 100%;
    box-sizing: border-box;
    height: 100px;
  }
  form button{
    display: block;
    margin: 20px auto 0 ;
    background:#2E8B57;
    padding: 10px;
    border: 0;
    font-size: 15px;
    border-radius: 7px;
    color: #fff;
  }
</style>