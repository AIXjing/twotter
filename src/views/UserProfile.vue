<template>
  <div class="user-profile">
    <div class="user-profile__user-panel">
      <h1 class="user-profile__username">@{{ user.username }}</h1>
      <div v-if="user.isAdmin" class="user-profile__admin-badge">
        Admin
      </div>
      <div class="user-profile__follower-count">
        <strong>Followers: </strong> {{ followers }}
      </div>
      <CreateTwootPanel @add-twoot="addTwoot"/>
    </div>

    <div class="user-profile__twoots-wrapper">
      <TwootItem
          v-for="twoot in user.twoots"
          :key="twoot.id"
          :twoot="twoot"
          :username="user.username"
          @favourite="toggleFavourite"
      />
    </div>
  </div>
</template>

<script>

import TwootItem from "../components/TwootItem";
import CreateTwootPanel from "@/components/CreateTwootPanel";

export default {
  name: 'UserProfile',
  components: {TwootItem, CreateTwootPanel},
  data() {
    return {
      followers: 0,
      user: {
        id: 1,
        username: '_Jing',
        firstName: 'Jing',
        lastName: 'Ai',
        email: 'aijing19910205@gmail.com',
        isAdmin: true,
        twoots: [
          {id: 1, content: "Twotter is Amazing!"},
          {id: 2, content: "Don't forget to subscriber to the earth is Square!"}
        ]
      }
    }
  },
  methods: {
    addTwoot(twoot) {
        this.user.twoots.unshift({
          id: this.user.twoots.length + 1,
          content: twoot
        })
      }
  }
}

</script>

<style lang="scss" scoped>
.user-profile {
  display: grid;
  grid-template-columns: 1fr 3fr;
  padding: 50px 5%;

  .user-profile__user-panel {
    display: flex;
    flex-direction: column;
    margin-right: 50px;
    padding: 20px;
    background-color: white;
    border-radius: 5px;
    border: 1px solid #DFE3E8;

    h1 {
      margin: 0
    }

    .user-profile__admin-badge {
      background: rebeccapurple;
      color: white;
      border-radius: 5px;
      margin-right: auto;
      margin-top: 5px;
      margin-bottom: 5px;
      padding: 0 10px;
      font-weight: bold;
    }

    .user-profile__create-twoot {
      padding-top: 20px;
      display: flex;
      flex-direction: column;

      &.--exceeded{
        color:red;
        border-color: red;
        button{
          background-color: red;
        }
      }
    }
  }

  .user-profile__twoots-wrapper {
    display: grid;
    grid-gap: 10px;
  }
}
</style>