<template>
  <div class="add-blog">
    <h2>添加博客</h2>
    <form v-if="!submitted">
        <label >博客标题</label>
        <input type="text" v-model="blog.title" required />
        <label >博客内容</label>
        <textarea v-model="blog.content"></textarea>
        <div id="checkbox">
            <label for="">Vue.js</label>
            <input type="checkbox" value="Vue.js" v-model="blog.categories">
            <label for="">Node.js</label>
            <input type="checkbox" value="Node.js" v-model="blog.categories">
            <label for="">React.js</label>
            <input type="checkbox" value="React.js" v-model="blog.categories">
            <label for="">Angular4</label>
            <input type="checkbox" value="Angular4" v-model="blog.categories">
        </div>
        <label for="">作者：</label>
        <select name="" id="" v-model="blog.author">
            <option v-for="author in authors" >
                {{author}}
            </option>
        </select>
        <button v-on:click.prevent="post">添加博客</button>

    </form> 
    <div id="preview">
        <h3>博客总览</h3>
        <p>博客标题</p>
        <p>{{blog.title}}</p>
        <p>博客内容:</p>
        <p>{{blog.content}}</p>
        <p>博客分类：</p>
        <ul>
            <li v-for="category in blog.categories">
                {{category}}
            </li>
        </ul>
        <p>作者：{{blog.author}}</p>
    </div>
  </div>
</template>

<script>
export default {
  name: 'add-blog',
  data () {
    return {
      blog:{
          title:"",
          content:"dajihao",
          categories:[],
          author:""
      },
      authors:["a","b","c"],
      submitted:false
    }
  },
  methods:{
      post:function (){
           this.$http.post("http://jsonplaceholder.typicode.com/posts",{title:this.blog.title,body:this.blog.content,userId:1})
              .then(function(data){
                     console.log(data);
                     this.submitted=true;
              }
              );
      }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
