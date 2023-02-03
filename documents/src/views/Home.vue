<template>
  <div class="home">
    <h1> Projects </h1>
    <div> <FilterNav @filterChange="current = $event" :current="current" :projects="projects"/> </div>

    <div  v-if="projects.length">
      <div v-for="project in filteredProjects" :key="project.id">
        <ShowProject :project="project" @delete="handleDelete" @complete="handleComplete" />
      </div>
    </div>
    <div>
      <p class="border1"> <span class="colorBlue"> Last update: </span> {{ time }} {{ date }} </p>
      <p id="pResult" class="border1"> 
        Click the title for see the details. You can delete, edit or add items 
        also you can change the theme to black or white with toggle icon.
      </p>
    </div>
    
  </div>
</template>

<script>
import ShowProject from "../components/ShowProject.vue";
import FilterNav from "@/components/FilterNav.vue";
  export default {
    name: 'Home',
    components: {
        ShowProject,
        FilterNav
    },
    
    data () {
      return {
        projects: [],
        current: "all",
        time: new Date().toLocaleTimeString(),
        date: new Date().toDateString(),
      }
    },
    // This means when the site first loaded, mounted will be a process...
    mounted () {
      fetch("http://localhost:3000/projects/")
        .then( res => res.json() )
        .then( data => this.projects = data )
        .catch( err => console.log(err.message) )
    },
    
    methods: {
      handleDelete ( id ) {
        this.projects = this.projects.filter( item => item.id !== id );
        document.querySelector("#pResult").classList.add("colorRed");
        document.querySelector("#pResult").innerHTML = "If no changing on the page, please refresh the page for see results.";
      },
      handleComplete ( id ) {
        let p = this.projects.find( item => item.id === id );
        document.querySelector("#pResult").classList.add("colorRed");
        document.querySelector("#pResult").innerHTML = "If no changing on the page, please refresh the page for see results.";
        p.isCompleted = !p.isCompleted;
      }
    },
    
    computed: {
      filteredProjects () {
        if ( this.current === "completed" ) {
          return this.projects.filter( item => item.isCompleted )
        }
        if ( this.current === "draft" ) {
          return this.projects.filter( item => !item.isCompleted )
      }
      return this.projects;  
      },
    }
  }
</script>

<style scoped>
h1 {
  color: #20639B;
  font-family: Cambria, Cochin, Georgia, Times, 'Times New Roman', serif;
}
.border1 {
    margin: 20px auto;
    background: #fff;
    padding: 10px 20px;
    border-radius: 5px;
    box-shadow: 10px 10px 10px rgba(0, 0, 0, 0.05);
    font-weight: bolder;
  
  }
.colorRed {
    color: red;
  }

.colorBlue {
  color:#20639B
}
</style>