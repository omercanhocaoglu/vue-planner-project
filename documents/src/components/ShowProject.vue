<template>
    <div class="project" :class="{complete: project.isCompleted}">
        <div class="actions">
            <h2 @click="showDetails"> {{ project.title }} </h2>
            <div class="icons">
                <router-link :to="{name:`EditProject`, params:{id: project.id}}" > <span class="material-symbols-outlined editIcon"> edit </span> </router-link>
                <span @click="toggleComplete" class="material-symbols-outlined doneIcon tick"> done </span>
                <span @click="deleteProject" class="material-symbols-outlined deleteIcon"> delete </span>
            </div>
        </div>
        <div class="details" v-if="seeDetails">
            <p> {{ project.details }} </p>
        </div>
    </div>
</template>

<script>
  export default {
       props: [
        "project"
       ],
       data () {
        return {
            seeDetails: false,
            uri: "http://localhost:3000/projects/" + this.project.id,
        }
       },
       methods: {
        showDetails () {
            return this.seeDetails = !this.seeDetails
        },
        deleteProject () {
            fetch(this.uri, { method: "DELETE" } )
            .then( () => this.$emit("delete"), this.project.id )
            .catch(err => console.log(err.message));
        },
        toggleComplete () {
          fetch(this.uri, {
            method: "PATCH",
            headers: {
              "Content-Type": "application/json",
            },
            body: JSON.stringify({
              isCompleted: !this.project.isCompleted
            })
          })
          .then(() => this.$emit("complete"), this.project.id )
          .catch(err => console.log(err.message));
        },
       },
    }
</script>

<style scoped>
.project {
    margin: 20px auto;
    background: #fff;
    padding: 10px 20px;
    border-radius: 5px;
    box-shadow: 10px 10px 10px rgba(0, 0, 0, 0.05);
    border-left: 5px solid #20639B;
}

h2 {
    cursor: pointer;
    user-select: none;
    text-transform: capitalize;
}

h2:hover {
  color: #20639B;
}

.actions {
    display: flex;
    justify-content: space-between;
    align-items: center;
}

.material-symbols-outlined {
  font-variation-settings:
  'FILL' 1,
  'wght' 400,
  'GRAD' 0,
  'opsz' 20px;
  font-size: large;
  margin-left: 5px;
  cursor: pointer;
  user-select: none;
  }

.deleteIcon {
    color: black;
  }

.deleteIcon:hover {
    color: red;
  }

.doneIcon {
    color: black;
  }

.doneIcon:hover {
    color: green;
  }

.editIcon {
    color: black;
  }

.editIcon:hover {
    color: #20639B;
  }

.project.complete {
    border-left: 5px solid rgb(9, 131, 9)
  }

.project.complete  .tick {
    color: rgb(9, 131, 9);
  }

.details p {
    text-transform: none;
  }
</style>
