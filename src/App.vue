<script>
  import {ref, onMounted} from 'vue'
  import axios from 'axios' 
  export default {
    data() {
        return {
            posts: [], 
            textSearch: "", 
            postContent: {}
          }
      }, 

    mounted() {
        axios.get("https://api.devall.com.br/api/v1/post") 
        .then((response) => {
          this.posts = response.data
          this.posts.map((element) => {
              axios.get(`https://api.devall.com.br/api/v1/post/clique/${element.id}`)
              .then((response) => {
                  element.url = response.data.url;
                  console.log(element.url);
              })
          })
        })
        .catch((err) => (console.log(err)));
        

      }, 
    methods: {
        inputTextSearch(e) {
            this.textSearch = e.target.value;
         },
        SearchApi() {
            axios.get(`https://api.devall.com.br/api/v1/post?search=${this.textSearch}`)
            .then((response) => (this.posts = response.data))
            .catch((err) => (console.log(err)));
        } 
      }
  } 

</script>

<template>
   <div class="container">
     <header>
         <div class="line-content flex flex-center color-menu-bar">
          <div class="menu-bar">
              <div>
                  <a class="logo">/dev/all</a>
              </div>
              <div class="menu-bar-options"> 
                  <ul><li _ngcontent-c0=""><a _ngcontent-c0="" class="menu-link" href="https://discord.gg/JyXzTcP" style="color: #1f8ef1;" target="_blank">Discord</a></li><li _ngcontent-c0=""><a _ngcontent-c0="" class="menu-link" href="https://taverna.devall.com.br" style="color: #00d6b4;" target="_blank">Taverna</a></li><li _ngcontent-c0=""><a _ngcontent-c0="" class="menu-link" href="https://revista.devall.com.br" target="_blank">Revista</a></li><li _ngcontent-c0=""><a _ngcontent-c0="" class="menu-link" href="/blogs">Blogs</a></li><!----><li _ngcontent-c0=""><a _ngcontent-c0="" class="menu-link" href="/sobre">Sobre</a></li><!----><li _ngcontent-c0=""><a _ngcontent-c0="" class="menu-link" href="/cadastro">Cadastre-se!</a></li><!----><li _ngcontent-c0=""><a _ngcontent-c0="" class="menu-link" href="/auth">Entrar</a></li><!----></ul>
              </div>
           </div>
        </div>
     </header>
     <main> 
       <div class="line-content flex flex-center space-top">
          <input type="text" v-model="textSearch" @input="inputTextSearch" class="space-around" placeholder="Encontre aqui">
          <button  @click="SearchApi"> 
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
          </button>
       </div>
       <div class="posts">
          <div v-for="post in posts" :key="post.id" class="post-container">
            <div class="box-post">
              <div class="post-body">
              <div class="line-content">
                <a v-bind:href="post.url"><span class="text-title"> {{ post.titulo }} </span></a>
              </div>
              <div class="line-content space-top text-body">
                <span class="sub-text"> {{ post.resumo }} </span>
              </div>
              <div class="line-content space-top">
                <div class="line-content">
                  <div class="line-content text-body">
                    Cliques: {{post.cliques}} 
                    {{post.dataPublicacao}} 
                  </div>
                </div>
                <div class="line-content text-body">
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
@import url('https://fonts.googleapis.com/css2?family=Montserrat:ital,wght@1,100;1,200&family=Roboto:ital@1&family=Share+Tech+Mono&display=swap');
  body {
    background-color: #1e1e2e;
  }
  div h2 {
   padding: 0 20px; 
  }

  ul {
      display: flex; 
      flex-direction: row;
      justify-content: space-around;
      list-style-type: none;

    }
  li {
    font-family: "Audiowide", sans-serif;
  } 
  li a {
      text-decoration: none;
      color: white;
  }

  div a {
      color: black;
  }

  header {
    border-bottom: 2px solid #fd5d93;
  }

  main div input {
    width: 80%;
    padding: 10px;
    border-radius: 8px;
    border: 0px;
  }

  .container {
    height: auto;
    width: 100%; 
    /*border: 1px solid red;*/
    margin: 0 auto;
  }
  .line-content {
    display: block;
    width: 100%;
  }

  .menu-bar {
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 15px 0px;
    width: 85%;
  } 
  .color-menu-bar {
      background-color: #27293d;
    }
  .logo {
    background: #000;
    color: #fff;
    padding: .2em;
    border-radius: 8px;
    font-size: 2em;
    font-family: "Audiowide", sans-serif;
    font-weight: 400;
    float: left;
    margin-left: 7%;
    font-display: swap;
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
      margin-top: 40px;
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
      /*border: 2px solid red;*/
  }
  
  .box-post {
    display: block; 
    width: 90%;
    background-color: #fff;
    height: auto;
    box-shadow: 1px 2px 5px white;
    border-radius: 10px;
  } 

  .post-body {
      padding: 45px 10px;
    }

  .text-title {
      font-size: 24px;
      font-weight: 800;
      font-family: 'Montserrat', sans-serif;
  }

  .text-body {
      font-family: 'Share Tech Mono', monospace;
    }

  .menu-bar-options {
    width: 60%;
  }
  

</style>
