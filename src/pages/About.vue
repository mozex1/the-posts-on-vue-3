<template>
    <div class="text_wrapper">
        <h1 class='title'>Эта страница была создана во имя практических навыков во Vue 3. </h1>
        <h3 class='subtitle'>И вроде бы что то получилось !</h3>
    </div>
    <div>
        <img :src='randomCatSrc' @click="changeImg" class="random_cat" alt="random cat"/>
        <p class="subtitle_img">Нажми на картинку, что бы ее поменять</p>
    </div>
</template>
<script>
import axios from 'axios';
export default {
    
    data() {
        return {
            randomCatSrc: '',
            loading: false,
        }
        
    },
    methods: {
        async fetchCat() {
            try {
                const response = await axios.get('http://aws.random.cat/meow');
                this.randomCatSrc = response.data.file;
                this.loading = false;
            }
            catch(e) {
                console.log('Error from server');
            } 
        },
        changeImg() {
            this.loading = true; 
            this.fetchCat();

              
        }
    },
    created() {
        this.fetchCat();
    },

}
</script>
<style scoped>
    .text_wrapper {
        padding: 100px;
    }

    .title {
        text-align: center;
    }
    .subtitle {
        margin-top: 5px;
        text-align: center;
        color: teal;
        font-weight: 300;
    }

    .subtitle_img {
        margin-top: 8px;
        text-align: center;
        font-weight: 300;
        font-size: 10px;
        color: teal;
        cursor: default;
    }

    .random_cat {
        display: block;
        margin: 0 auto;
        width: 200px;
        height: 200px;
        border-radius: 10px;
    }

</style>