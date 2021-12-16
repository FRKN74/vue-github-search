<template>
  <div class="container">
    <label class="topTitle justify-content-center d-flex mt-2"> Github Profil | Search </label>
    <div class="row">
      <div class="col md-6 justify-content-center d-flex mt-5">
          <div class="form-group">
              
                  <input type="text" class="inputSearch" v-model="userSearch" /> 
                  <br>
                  <button class="btn btn-secondary ml-2 mb-2 btn-lg w-75 mx-auto mt-2 justify-content-center d-flex" @click="search()">Ara</button> 
              
          </div>
          <br>
      </div>
    </div>
    <hr class="style-three">
      <transition name="profil" :style="this.profilStyle">
        <div class="row">
              <div class="col md-6 justify-content-center d-flex ">
                    <div class="profil-card mb-3"  >
                      <a v-for="user in data" :key="user" :href="user.html_url" target="_blank">
                        <img :src="user.avatar_url" alt="" class="rounded mx-auto d-block mt-2 w-25">
                        </a>
                      <hr class="style-three">
                      <div class="labelCenter">
                          <a v-for="user in data" :key="user" :href="user.html_url" target="_blank"><label class="userName" >{{ user.login }}</label></a> 
                          <br>
                          <label class="user" v-for="user in data" :key="user">{{ user.name }}</label>
                      </div>   
                      <strong>
                        <label >{{ this.reposLenght }}</label>
                      </strong>
                      <hr class="style-three">
                      <div class="Repositories ml-3 mr-3">
                        <a v-for="(repos,index) in reposData" :key="index" :href="repos.html_url" target="_blank" >
                          <div class="repos" >
                            <label class="reposName ml-2 mr-2" >{{ repos.name }}</label>
                          </div>
                        </a>
                      </div> 
                    </div>
              </div>
          </div>
      </transition>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  data() {
    return {
      userSearch : null,
      data : {},
      reposData : {},
      profilStyle: "display:none",
    }
  },
  methods: {
    search(){
      axios.get('https://api.github.com/users/'+this.userSearch).then((Response) => {
        this.data = Response;
      });

      axios.get('https://api.github.com/users/'+ this.userSearch + '/repos').then((Response) => {

        this.reposData = Response.data;
        this.profilStyle ="display:block";
      });
    },
  },
}
</script>

<style>
*{
  padding: 0;
  margin: 0;
  box-sizing: border-box;
}
body{
  background-color: rgb(213, 221, 145);
}
.topTitle{
  color: rgb(73, 70, 70);
  text-decoration: underline;
  font-size: 21px;
}
.inputSearch{
  height: 60px;
  width: 800px;
  border-radius: 15px 15px;
  border: 1px solid #0277bd;
  background-color: rgb(58, 52, 52);
  outline: none;
  outline-style: none;
  color: white;
  padding-left:400px ;
  transition:  all .5s;
}
.inputSearch:hover{
  border-color: darkgray;
  background-color: #5A6268 ;
  outline: none;
  transition:  all .5s;
}

.profil-card{
  background-color: rgb(58, 52, 52);
  border: 1px solid rgb(150, 91, 91);
  height: auto;
  width: auto;
  border-radius: 20px;
  box-shadow: 0px 5px 20px 5px brown;
}
.image{
    margin-left: 420px;
    border-radius: 20px ;
}
.labelCenter{
  text-align: center;
}
.userName{
  color:#f0f0f0;
  transition:  all .8s;
}
.userName:hover{
  color: rgb(255, 255, 255);
  transform: translate(0px);
  transform: scale(1.5);  
  transition:  all .8s;
}
.userName:hover{
  text-decoration: underline;
  cursor: pointer;
}
.user{
  color:rgb(213, 221, 145);
}
.Repositories{
  display: flex;
  height: auto;
  width: auto;
  flex-wrap: wrap;
}
.repos{
  margin:10px;
  min-height: 30px;
  min-width: 100px;
  border: 1px solid rgb(58, 52, 52);
  border-radius:5px 5px;
  background-image: linear-gradient(to right ,#38523a ,darkgray);
  transition:  all .4s;
}
.reposName{
  color: white;
}
.reposName:hover{
  cursor: pointer;
}
.repos:hover{
    transform: translate(0px);
    transform: scale(1.1);
    transition:  all .4s;
}

hr.style-three {
height: 30px;
border-style: solid;
border-color: darkgrey;
border-width: 1px 0 0 0;
border-radius: 20px;
}
hr.style-three:before {
display: block;
content: "";
height: 30px;
margin-top: -31px;
border-style: solid;
border-color: darkgrey;
border-width: 0 0 1px 0;
border-radius: 20px;
}
  


</style>
