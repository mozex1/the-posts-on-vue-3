<template>
    <div>
        <h1 class="title">Это страница поста с ID: {{$route.params.id}}</h1>
        <my-button @click="$router.push('/posts')" class="button">Вернуться назад</my-button>
    </div>
</template>
<script>
export default {
    
}
</script>
<style scoped>
    .title {
        text-align: center;
        margin-top: 110px;
    }

    .button {
        display:block;
        margin: 30px auto 0 auto;
    }
</style>