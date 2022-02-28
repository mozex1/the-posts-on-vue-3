<template>
    <div class="post">
        <div>
            <div><strong>Название: </strong>{{post.title}}</div>
            <div class="text-bot" ><strong>Описание: </strong>{{post.body}}</div>
        </div>
        <div class="post__btns">
            <my-button @click="$router.push(`/posts/${post.id}`)" >Открыть</my-button>
            <my-button @click="$emit('remove', post)" >Удалить</my-button>
        </div>
    </div>
</template>

<script>
export default {
    props: {
        post: {
            type: Object,
            required: true,
        }
    },
}
</script>

<style scoped>
    .post {
        display:flex;
        align-items: center;
        justify-content: space-between;
        margin-top: 15px;
        padding: 20px;
        border: 2px solid teal;
    }

    .post__btns {
        display: flex;
    }

    .text-bot {
        margin-top: 5px;
        margin-right: 80px;
    }
</style>