<template>
    <div  id="show-blogs">

         <h1>List Blog Titles</h1>
         <input type="text" placeholder="Search blogs" v-model="search">
         <div class="single-blog" v-for="blog in filteredBlogs" :key="blog.index" >
                 <h2 v-rainbow>{{blog.title | to-uppercase}}</h2> 
                 <article>{{blog.body | snippet}}</article>
         </div>

   </div>
</template>


<script>
import searchMixins from '@/mixins/searchMixins'
export default {


    data(){
        return{
            blogs:[],
            search:'',
        }
    },
    methods:{
                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 

    },
    created(){
        this.$http.get('https://jsonplaceholder.typicode.com/posts').then(function(data){
            this.blogs = data.body.slice(0,10);
        }) 
    },
    computed:{
        
    },
    filters:{
        // 'to-uppercase':function(value){
        //     return value.toUpperCase();
        // }
        toUppercase(value){
            return value.toUpperCase();
        },
        snippet(value){
            return value.slice(0,100) + '...'
        }
    },

    directives:{
        'rainbow':{
            bind(el){
                el.style.color = '#'+ Math.random().toString().slice(2,8);
            }
        }
    },
    mixins:[searchMixins]
    
}
</script>

<style scoped>
    #show-blogs{
        max-width:800px;
        margin:0 auto;
    }
    .single-blog{
        padding: 20px;
        margin:  20px 0;
        box-sizing:border-box;
        background: #eee ;
    }
    input[type='text']{
        width: 100%;
        display: block;
        margin: 0 auto;
    }
</style>