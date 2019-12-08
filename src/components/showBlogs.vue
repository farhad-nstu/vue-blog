<template>
    <div v-theme:column="'narrow'" id="show-blogs">
        <h1>All Blog Articles</h1>
        <input type="text" v-model="search" placeholder="search blogs" />
        <div v-for="blog in filteredBlogs" class="single-blog">
            <router-link v-bind:to="'/blog/' + blog.id" rainbow><h2>{{ blog.title }}</h2></router-link>
            <article>{{ blog.body | snippet }}</article>
        </div>
    </div>
</template>

<script>
export default {
    data () {
        return {
            blogs: [],
            search: ''
        }
    },
    methods: {
    },
    created() {
        this.$http.get('http://jsonplaceholder.typicode.com/posts').then(function(data){
            this.blogs = data.body.slice(0,10);
        });
    },

    computed: {

        //Search function start
        filteredBlogs: function(){
            return this.blogs.filter((blog) => {
                return blog.title.match(this.search);
            });
        }
        //Search function end
    },

    filters: {
        toUpperCase(value){
            return value.toUpperCase();
        },
        snippet(value){
            return value.slice(0,200) + '...';
        }
    },

    directives: {
        'rainbow' :{
            bind(el, binding, vnode){
                el.style.color = "#" + Math.random().toString(16).slice(2, 8);
            }
        },

        'theme' : {
            bind(el, binding, vnode){
                if (binding.value == 'wide'){
                    el.style.maxWidth = "1260px";
                } else if (binding.value = 'narrow'){
                    el.style.maxWidth = "560px";
                }
                if(binding.arg == 'column'){
                    el.style.background = '#ddd';
                    el.style.padding = '20px';
                }
            }
        }
    }


}
</script>

<style>
#show-blogs{
    max-width: 800px;
    margin: 0px auto;
}
.single-blog{
    padding: 20px;
    margin: 20px 0;
    box-sizing: border-box;
    background: #eee;
}
</style>