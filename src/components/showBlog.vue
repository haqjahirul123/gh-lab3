<template>
  
    <div id="show-blogs">
        <div class="container">
        <button  @click="latestData()" class="latestBtn">LatestData</button>
        </div>
        <h1>Show All Title And Content At Blog </h1>
        <div v-for="blog in blogs"  :key="blog.id"  class="single-blog">
            <h2>{{ blog.title }}</h2>
            <article>{{ blog.content }}</article>
            
            <button  @click="del(blog.id)" class="delBtn">Detete</button>
            
        </div>
    </div>
</template>

<script>
export default {
    data () {
        return {
            blogs: []
        }
    },
    methods: {
        del(id ){
            this.$http.post('https://www.forverkliga.se/JavaScript/api/api-snippets.php?delete',{
                delete:"",
                id:id
            }).then(function(data){
                console.log(data);
                // this.submitted = true;
                location.reload();
             }).catch(function(error){
                 console.log(error);
             })
        },
        latestData() {
        this.$http.get('https://www.forverkliga.se/JavaScript/api/api-snippets.php?latest')
        .then(function(data){
            this.blogs = data.body.slice(0,20);
        });
    }
    },
    // created() {
    //     this.$http.get('https://www.forverkliga.se/JavaScript/api/api-snippets.php?latest')
    //     .then(function(data){
    //         this.blogs = data.body.slice(0,20);
    //     });
    // }
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
    background: rgb(158, 154, 154);
}
.delBtn{
    background-color:rgb(197, 97, 61);
    width: auto;
    border: rgb(255, 36, 7);
   
}
.container { 
  height: 50px;
  position: relative;
  border: 3px solid green; 
}

.latestBtn {
  margin: 0;
  width: 50%;
  height: 2em;
  background-color: chartreuse;
  position: absolute;
  top: 50%;
  left: 50%;
  -ms-transform: translate(-50%, -50%);
  transform: translate(-50%, -50%);
}
</style>