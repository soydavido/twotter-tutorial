<template>
    <div class="user-profile"> 
        <div class="user-profile_user-panel">
            <h1 class="user-profile_username">@{{user.username}}</h1>
            <div class="user-profile_admin-badge" v-if="user.isAdmin">
                Admin
            </div>
            <div class="user_profile_follower_count">
                <strong>Followers: </strong>{{followers}}
            </div>
        </div>
        <div class="user-profile_twoots-wrapper">
            <TwootItem 
                v-for="twoot in user.twoots" 
                :key="twoot.id" 
                :username="user.username" 
                :twoot="twoot" 
                @favourite="toggleFavourite"
            />
        </div>
    </div>
</template>

<script>
//<TwootItem v-for="twoot in user.twoots" :key="twoot.id" :username="user.username" :twoot="twoot"/>
import TwootItem from "./TwootItem"

export default {
  name: 'UserProfile',
  components: { TwootItem },
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
        twoots: [
            {id: 1, content: 'Twotter is amazing'},
            {id: 2, content: '[ as ]'}
        ]
        //,followers: 0,
        //following: 0
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
    },
    toggleFavourite(id){
        console.log(`Favourited Twoot #${id}`)
    }
  },
  mounted(){   //Cuando se construya el componente se correra todo lo que este aqui
    this.followUser();
  }
}
</script>

<style>
.user-profile {
    display: grid;
    grid-template-columns: 1fr 3fr;
    width: 100%;
    padding: 50px 5%;
}

.user-profile_user-panel{
    display: flex;
    flex-direction: column;
    margin-right: 50px;
    padding: 20px;
    background-color: white;
    border-radius: 5px;
    border: 1px solid #DFE3E8;
}

.user-profile_admin-badge{
    background: rebeccapurple;
    color: white;
    border-radius: 5px;
    margin-right: auto;
    padding: 0 10px;
}
h1{
    margin: 0;
}
</style>