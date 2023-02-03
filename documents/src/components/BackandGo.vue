<template>
    <div class="forBackandGo">
        <span @click="Back"> Back </span> |
        <span @click="Home"> Home </span> |
        <span @click="Forward"> Forward </span> |
    </div>
</template>

<script>
    export default {
        methods: {
            Back () {
                this.$router.go(+1)
            },
            Home () {
                this.$router.push({ name: "home" })
            },
            Forward () {
                this.$router.back(-1)
            }
        },
    }
</script>

<style scoped>
.forBackandGo {
    text-align: center;
    font-size: small;
    user-select: none;
    cursor: pointer;
}

span:hover {
    color: #20639B;
    font-weight: bold;
}

</style>