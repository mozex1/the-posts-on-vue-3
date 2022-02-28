<template>
    <form class="form" @submit.prevent>
        <h4>Добавить новый пост</h4>
        <my-input 
            v-focus
            v-model="post.title"
            type="text" 
            placeholder="Название"/>
        <!-- <my-input 
            v-model:value="post.title"
            v-model:myvalue="post.title"
            type="text" 
            placeholder="Название"/> -->
        <my-input 
            v-model="post.body"
            type="text" 
            placeholder="Небольшое описание"/>
        <my-button style="margin-top: 15px;" @click="createPost">Опубликовать</my-button>
    </form>
</template>

<script>

export default {
    data() {
        return {
            post: {
                title: '',
                body: '',
            }
        }
    },
    methods: {
        createPost() {
            this.post.id = Date.now();
            if(this.post.title && this.post.body) {
                this.$emit('create', this.post);
            }
            this.post = {
                title: '',
                body: '',
            }
        },
    },
    
}
</script>
<style scoped>
    .form {
        display: flex;
        flex-direction: column;

    }
</style>