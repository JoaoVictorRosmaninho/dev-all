<script>
  import {ref, onMounted} from 'vue'
  import axios from 'axios' 
  export default {
    data() {
        return {
            posts: []
          }
      }, 

    mounted() {
        axios.get("https://api.devall.com.br/api/v1/post") 
        .then((response) => (this.posts = response.data))
        .catch((err) => (console.log(err)));
      }
  } 

</script>

<template>
   <div class="container">
     <header>
         <div class="line-content flex flex-between">
            <h2>/dev/all</h2>
            <h2>Taverna</h2>
         </div>
     </header>
     <main> 
       <div class="line-content flex flex-center space-top">
          <input type="text" class="space-around" placeholder="Encontre aqui">
          <svg 
          xmlns="http://www.w3.org/2000/svg" 
          width="16" 
          height="16" 
          fill="currentColor" 
          class="bi bi-search space-around" 
          viewBox="0 0 16 16">
              <path 
                d="M11.742 10.344a6.5 6.5 0 1 0-1.397 1.398h-.001c.03.04.062.078.098.115l3.85 3.85a1 1 0 0 0 1.415-1.414l-3.85-3.85a1.007 1.007 0 0 0-.115-.1zM12 6.5a5.5 5.5 0 1 1-11 0 5.5 5.5 0 0 1 11 0z"/>
      </svg>
       </div>
       <div class="posts">
          <div v-for="post in posts" :key="post.id" class="post-container">
            <div class="box-post">
              <div class="post-body">
              <div class="line-content">
                <span class="text-title"> {{ post.titulo }} </span>
              </div>
              <div class="line-content space-top">
                <span class="sub-text"> {{ post.resumo }} </span>
              </div>
              <div class="line-content space-top">
                <div class="line-content">
                  <div class="line-content">
                    Cliques: {{post.cliques}} 
                    {{post.dataPublicacao}} 
                  </div>
                </div>
                <div class="line-content">
                  Em: <a href="#">{{post.blog.nome}}</a>
                </div>
              </div>
             </div>
            </div>
          </div>
        </div>
     </main>
   </div>
</template>

<style>
  
  div h2 {
   padding: 0 20px; 
  }

  header {
    border-bottom: 2px solid black;
  }

  main div input {
    width: 60%;
    padding: 5px;
  }

  .container {
    height: auto;
    width: 100%; 
    border: 1px solid red;
    margin: 0 auto;
  }
  .line-content {
    display: block;
    width: 100%;
  }
  
  .flex {
    display: flex;
  }

  .flex-between {
    justify-content: space-between;
  }
  .flex-center {
    justify-content: center;
    align-items: center;
  }
  
  .space-top {
      margin-top: 20px;
  }
  .space-around {
      margin: 0 5px;
  }

  .posts {
    margin-top: 50px;
  }
  .post-container {
      width: 100%; 
      height: auto;
      padding: 5px 60px;
      border: 2px solid red;
  }
  
  .box-post {
    display: block; 
    width: 90%;
    height: auto;
    box-shadow: 1px 2px 5px gray;
    border-radius: 10px;
  } 

  .post-body {
      padding: 45px 10px;
    }

  .text-title {
      font-size: 24px;
      font-weight: 800;
  }
  

</style>
