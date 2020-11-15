<template>
 <div class="user-profile">
  <div class="user-profile_user-panel">
   <h1 class="user-profile_username">@{{ user.username }}</h1>
   <div class="user-profile_admin-badge" v-if="user.isAdmin">
       Admin
   </div>
   <div class="user-profile_follower-count">
    <strong>Followers: </strong> {{ followers }}
   </div>
  </div>
  <div class="user-profile_twoots-wrapper">
   <TwootItem v-for="twoot in user.twoots" :key="twoot.id" :username="user.username" :twoot="twoot" @favorite="toggleFavorite"/>
  </div>
 </div>
</template>

<script>
import TwootItem from "./TwootItem";

export default {
  name: 'UserProfile',
  components: { TwootItem },
  data() {
    return {
      followers: 0,
      user:{
        id: 1,
        username: 'josephcgolden',
        firstName: 'Joseph',
        lastName: 'Chretien-Golden',
        email: 'joechre@gmail.com',
        isAdmin: true,
        twoots: [
            {id: 1, content: 'Twotter is Amazing!'},
            {id: 2, content: "Don't forget to subscribe to the my channel!"}
        ]
      }
    }
  },
  watch: {
    followers(newFollowerCount, oldFollowerCount) {
      if (oldFollowerCount < newFollowerCount) {
        console.log(`${this.user.username} has gained a follower`)
      }
    }
  },
  computed: {
    fullName() {
      return `${this.user.firstName} ${this.user.lastName}`;
    }
  },
  methods: {
    followUser() {
      this.followers++
    },
    toggleFavorite(id) {
        console.log(`Favorited Tweet #${id}`)
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

.user-profile_user-panel {
    display: flex;
    flex-direction: column;
    margin-right: 50px;
    padding: 20px;
    background-color: white;
    border-radius: 5px;
    border: 1px solid #DFE3E8;
}

.user-profile_admin-badge {
    background: rgb(122, 194, 236);
    color: white;
    border-radius: 5px;
    margin-right: auto;
}

h1 {
    margin: 0;
}
</style>
