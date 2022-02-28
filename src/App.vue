<template>
    <div class="main">
        <navbar></navbar>
        <div class="app">
            <router-view></router-view>
        </div>
    </div>
</template>
<script>
import Navbar from "@/components/Navbar";
export default {
    components: {
        Navbar
    }
}
</script>
<style>
    * {
        margin: 0;
        padding: 0;
        box-sizing: border-box;
        font-family: 'Roboto', sans-serif;
    }
    .main {
        padding:0 100px 0 100px;
        
    }
    .app {
        padding: 20px;
        /* background-color: rgba(128,128,128, 0.1); */
    }

</style>