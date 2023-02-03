<template>
  <div class="about">
    <h1>Add New Project </h1>

    <div>
      <form @submit.prevent="handleSubmit">
        <input type="text" placeholder="Text here for title!" v-model="title">
        <br> <br>
        <textarea v-model="details" placeholder="Text here for details!"></textarea>
        <br>
        <button class="forAddButton"> Add Project </button>
        <p id="p1"></p>
      </form>
    </div>
  </div>
</template>

<script>
  export default {
    
    data () {
      return {
        title: "",
        details: "",
        uri: "http://localhost:3000/projects/"
      }
    },
    methods: {
      handleSubmit () {
        let project= {
          title: this.title,
          details: this.details,
          isCompleted: false,
        };
        fetch(this.uri, {
          method: "POST",
          headers: {
              "Content-Type": "application/json",
            },
          body: JSON.stringify(project)
        })
        .then( () => this.$router.push("/") )
        .catch(err => console.log(err.message));
        this.title= "" , this.details= "";
      }
    },
  }
</script>

<style scoped>
input {
    margin: 20px auto;
    background: #fff;
    padding: 10px 20px;
    border: 0;
    border-bottom: 2px solid black;
    border-radius: 5px;
    box-shadow: 10px 10px 10px rgba(0, 0, 0, 0.05);
    font-weight: bolder;
    width: 50%;
}

textarea {
    margin: 20px auto;
    background: #fff;
    padding: 10px 20px;
    border: 0;
    border-bottom: 2px solid black;
    border-radius: 5px;
    box-shadow: 10px 10px 10px rgba(0, 0, 0, 0.05);
    font-weight: bolder;
    width: 100%;
}


button {
  margin: 20px auto;
    background: #fff;
    padding: 10px 20px;
    border: 1px solid black;
    border-bottom: 2px solid black;
    border-radius: 5px;
    box-shadow: 10px 10px 10px rgba(0, 0, 0, 0.05);
    font-weight: bolder;
    width: 20%;
    color: #20639B;
}

h1 {
  color: #20639B;
  font-family: Cambria, Cochin, Georgia, Times, 'Times New Roman', serif;
}
</style>