<template>
    <input :class="{search_panel: isSearchPanel }" :value="modelValue" @input="updateInput" class="input" type='text'>
</template>

<script>
export default {
   
    name: 'my-input',
    data() {
        return {
            
        }
    },
    props: {
        modelValue: [String, Number],
        isSearchPanel: Boolean,

    },
    methods: {
        updateInput(event) { // Можно было написать в самом @input
            this.$emit('update:modelValue', event.target.value)
        }
    },

}
</script>

<style scoped>
    .input {
        width: 100%;
        border: 1px solid teal;
        border-color: teal;
        padding: 10px 15px;
        margin-top: 15px;
    }
    .input:focus {
        outline: 0;
        border-color: teal;
        background-color: white;
    }

    .search_panel {
        width: 100%;
        border: 1px solid white;
        background-color: rgba(128,128,128, 0.1);
        padding: 10px 15px;
        margin-top: 15px;
    } 

    .search_panel:focus {
        color: black;
        border-color: teal;
        outline: 0;
        background-color: white;
        }
</style>