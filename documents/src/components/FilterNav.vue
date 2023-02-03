<template>
    <div>
        <nav class="filter-nav">
            <button @click="updateFilter(`all`)" :class="{active: current === `all`}"> All ({{ projects.length }}) </button>
            <button @click="updateFilter(`completed`)" :class="{active: current === `completed`}"> Completed </button>
            <button @click="updateFilter(`draft`)" :class="{active: current === `draft`}"> Draft </button>
        </nav>
    </div>
</template>

<script>
    export default {
        props: [
            "current",
            "projects"
        ],

        methods: {
            updateFilter(by) {
                this.$emit( "filterChange", by ) 
            }
        },
    }
</script>

<style scoped>
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
    color: black;
    margin: 2px;
    cursor: pointer;
}

button.active {
    color: #20639B;
}
</style>