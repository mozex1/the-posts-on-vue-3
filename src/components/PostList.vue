<template>
    <div v-show="posts.length > 0">
        <h3>Список постов</h3>
        <transition-group name='list'>
            <PostItem 
                v-for="post in posts"
                :post="post" 
                :key="post.id"
                @remove="$emit('remove', post)"
            />
        </transition-group>
        
    </div>
    <h2 v-show="posts.length === 0" style="color: DarkSlateGray; text-align: center">Список постов пока пуст</h2>
    
</template>

<script>
import PostItem from "@/components/PostItem";
export default {
    components: {PostItem},
    props: {
        posts: {
            type: Array,
            required: true
        }
    }
}
</script>
<style scoped>
    .list-move,
    .list-enter-active,
    .list-leave-active {
    transition: all 0.4s ease;
    }

    .list-enter-from,
    .list-leave-to {
    opacity: 0;
    transform: translateX(30px);
    }

    .list-leave-active {
    position: absolute;
    }
</style>