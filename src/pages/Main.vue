<template>
    <div>
        <div class="text_wrapper">
            <h1 class="title">Привет, друг!</h1>
            <h3 class="subtitle">Добро пожаловать на этот учебный проект по Vue 3, в котором я только начал знакомство с ним! </h3>
            <my-matrix-screen></my-matrix-screen>
        </div>
    </div>
</template>
<script>
export default {
    
}
</script>
<style scoped>
    .text_wrapper {
        padding: 100px;
        text-align: center;
    }

    .subtitle {
        margin-top: 5px;
        color: teal;
        font-weight: 300;
    }
</style>