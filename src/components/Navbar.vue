<template>
    <div class="navbar_wrapper">
        <div class="navbar">
            <img src="@/img/star.svg" @click="$router.push('/')" class="logo" alt="img"/>
            <div class="main_link" @click="$router.push('/')">Главная</div>
            <div class="navbar__btns">
                <my-button @click="$router.push('/posts')">Посты</my-button>
                <my-button @click="$router.push('/about')" style="margin-left: 15px;">О сайте</my-button>
                <!-- <my-button @click="$router.push('/store')" style="margin-left: 15px;">Хранилище</my-button>
                <my-button @click="$router.push('/composition')" style="margin-left: 15px;">Composition API</my-button> -->
            </div>
        </div>
    </div>
</template>
<script>
export default {
    
}
</script>
<style scoped>
    /* .navbar_wrapper{
        padding: 0 20px;
    } */

    .logo {
        margin-right: 5px;
        width: 50px;
        height: 50px;
        cursor: pointer;
    }

    .navbar {
        display: flex;
        height: 60px;
        background-color: rgba(0, 128, 128, 0.2);
        align-items: center;
        padding: 0 15px;
        border-radius: 5px;
    }

    .navbar__btns {
        margin-left: auto;
    }

    .main_link{
        cursor: pointer;
        font-weight:500;
    }
</style>