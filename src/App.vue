<template>
  <div id="app">
      @{{user.username}} - {{fullName}}
      <div>
        <strong>Followers:</strong> {{this.followers}}
      </div>
      <button @click="followUser">Follow</button>
  </div>
</template>

<script>


export default {
  name: 'App',
  data(){
    return{
      followers: 0,
      user:{
        id: 1,
        username: 'soydavido',
        firstName: 'David',
        lastName: 'Ortuño',
        email: 'ortuod@gmail.com',
        isAdmin: true, 
        followers: 0,
        following: 0
      }
    }
  },
  watch: {
    followers(newFollowerCount, oldFollowerCount) {
      if (oldFollowerCount < newFollowerCount){
        console.log(this.user.username+' has gained a follower')
      }
    }
  },
  computed: {
    fullName(){
      //return `${this.user.firstName} ${this.user.lastName}` Strings literales
      return this.user.firstName + ' ' + this.user.lastName
    }
  },
  methods: {
    followUser(){
      this.followers++
    }
  },
  mounted(){   //Cuando se construya el componente se correra todo lo que este aqui
    this.followUser();
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
  display: flex;
  flex-direction: column;
}
</style>
