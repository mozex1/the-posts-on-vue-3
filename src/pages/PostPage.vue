<template>
    <div>
        <h1>Страница с постами</h1>
        <my-input v-focus v-model="searchQuery" class="search_panel" :is-search-panel="true" placeholder="Поиск ..."/>
        <div class="app__btns">
            <my-button @click="showDialog">Создать пост</my-button>
            <my-select 
            v-model="selectedSort" 
            :options="sortOptions"
            ></my-select>
        </div>
        
        <my-dialog v-model:show="dialogVisible">
            <PostForm 
            @create="createPost"
        /></my-dialog>

        <PostList 
        :posts="sortedAndSearchPosts"
        @remove="removePost"
        v-if="!isPostsLoading"
        />
        <div v-else class="loading">
            <my-loader></my-loader>
            <div class="loading__text">Загрузка постов ...</div>
        </div>

        <div v-intersection="loadMorePosts" class="observer"></div>
        <!-- <div class="page__wrapper"> // Функционал постраничной навигации по постам
            <div 
            v-for="pageNumber in totalPages" 
            :key="pageNumber" 
            class="page"
            :class="{'current-page': page === pageNumber}"
            @click="changePage(pageNumber)"
            >{{pageNumber}}</div>
        </div> -->
        
    </div>
</template>

<script>
    import PostForm from '@/components/PostForm';
    import PostList from '@/components/PostList';
    import axios from 'axios';
    export default {
        components: {
            PostForm, PostList,
        },
        data() {
            return {
                posts: [],
                dialogVisible: false,
                modificatorValue: '',
                isPostsLoading: false,
                selectedSort: '',
                searchQuery: '',
                page: 1,
                limit: 10,
                totalPages: 0,
                sortOptions: [
                    {value: 'title', name: 'По названию'},
                    {value: 'body', name: 'По описанию'},
                ],
            }
        },
        methods: {
            createPost(post){
               this.posts.push(post); 
               this.dialogVisible = false;
            },
            removePost(post){
                this.posts = this.posts.filter(p => p.id !== post.id)
            },
            showDialog() {
                this.dialogVisible = true;
            },
            // changePage(pageNumber) { // Функционал постраничной навигации по постам
            //     this.page = pageNumber;
            // },
            async fetchPosts() {
                try {
                    this.isPostsLoading = true;
                    const response = await axios.get('https://jsonplaceholder.typicode.com/posts', {
                        params: {
                            _page: this.page,
                            _limit: this.limit
                        }
                    });
                    // const response = await axios.get('https://kitsu.io/api/edge/manga');
                    // this.posts = response.data.data;
                    this.totalPages = Math.ceil(response.headers['x-total-count'] / this.limit);
                    this.posts = response.data;
                        
                }
                catch(e) {
                    console.log('Error from server');
                } finally {
                    this.isPostsLoading = false;
                }
            },
            async loadMorePosts() {
                try {
                    this.page += 1;
                    const response = await axios.get('https://jsonplaceholder.typicode.com/posts', {
                        params: {
                            _page: this.page,
                            _limit: this.limit
                        }
                    });
                    this.totalPages = Math.ceil(response.headers['x-total-count'] / this.limit);
                    this.posts = [...this.posts, ...response.data];
                        
                }
                catch(e) {
                    console.log('Error from server');
                } finally {
                    console.log('got new posts');
                }
            },
        },
        mounted() {
            this.fetchPosts();
        },
        computed: {
            sortedPosts() {
                return [...this.posts].sort((post1, post2) => {
                    return post1[this.selectedSort]?.localeCompare(post2[this.selectedSort]);
                });
            },
            sortedAndSearchPosts() {
                return this.sortedPosts.filter(post => post.title.toLowerCase().includes(this.searchQuery.toLowerCase()));
            }
        },
        watch: {
            // page() { // Функционал постраничной навигации по постам
            //     this.fetchPosts();
            // }
        }
    }
</script>

<style>
    .app__btns {
        margin: 15px 0;
        display: flex;
        justify-content: space-between;
    }

    .page__wrapper {
        display: flex;
        justify-content: center;
        margin-top: 30px;
    }

    .page {
        border: 1px solid rgb(0,128,128, 0.5);
        cursor: pointer;
        border-radius: 3px;
        padding: 10px;
        margin-left: 10px;
        transition: 0.5s all;
    }
    .page:nth-of-type(1) {
        margin-left: 0px;
    }
    .page:hover {
        transform: scale(115%);
    }

    .current-page {
        border: 2px solid teal;
    }

    .loading {
        margin-top: 50px;
        display:flex;
        flex-direction:column;
    }

    .loading__text {
        margin: 70px 0 0 10px;
        text-align: center;
        font-size: 20px;
        font-weight: 600;
    }

    .observer {
        background: rgba(0,0,0,0);
    }


</style>