<template>
  <div class="user-profile">
    <div class="user-profile__user-panel">
      <h1 class="user-profile__username">@{{ user.username}}</h1>
      <div class="user-profile__admin-badge" v-if="user.isAdmin">
        Admin
      </div>
      <div class="user-profile__follower-count">
        <strong>Followers: </strong> {{ followers }}
      </div>
    </div>
    <div class="user-profile__twoots-wrapper">
      <div class="user-profile_twoot" v-for="twoot in user.twoots" :key="twoot.id">
        {{ twoot.content}}
      </div>
    </div>
  </div>

  <!-- <button @click="followUser">        @click ist das gleiche wie v-on:click
     Follow
   </button> -->

</template>

<script>
export default {
name: "UserProfile",
  data(){
    return{
      followers: 0,
      user: {
        id: 1,
        username: '_praeses',
        firstname: 'Celine',
        lastname: 'Correngourt',
        email: 'celine.correngour@mail.ch',
        isAdmin: true,
        twoots: [
          {id: 1, content: 'Twotter is amazing!'},
          {id: 2, content: 'Subscribe to meee!'}
        ]
      }
    }
  },
  watch: {
    followers(newFollowerCount, oldFollowerCount){
      if(oldFollowerCount < newFollowerCount){
        console.log(`${this.user.username} has gained a follower!`)
      }
    }
  },
  computed: {
    fullName() {
      return `${this.user.firstname} ${this.user.lastname}`;
    }
  },
  methods: {
    followUser() {
      this.followers++
    }
  },
  mounted() {
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
.user-profile__user-panel {
  display: flex;
  flex-direction: column;
  margin-right: 50px;
  padding: 20px;
  background-color: white;
  border-radius: 5px;
  border: 1px solid #DFE3E8;
}

h1 {
  margin: 0;
}
.user-profile__admin-badge {
  background: rebeccapurple;
  color: white;
  border-radius: 5px;
  margin-right: auto;
  padding: 0 10px;
  font-weight: bold;
}

</style>