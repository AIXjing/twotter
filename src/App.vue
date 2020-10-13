<template>
  <div id="app" v-if="user">
    <nav>
      <router-link to="/">
        <div class="navigation__logo">
          Twotter
        </div>
      </router-link>
      <router-link :to="{name: 'UserProfile', params: { userId: user.id } }">
        <div class="navigation__user" v-if="user">
          {{ user.username }}
        </div>
      </router-link>
    </nav>
    <!--Add router here to use router-->
    <router-view/>
  </div>
</template>

<script>
import {useStore} from 'vuex';
import {computed} from 'vue';

export default {
  name: 'App',
  setup() {
    const store = useStore();
    const user = computed (() => {
      console.log("App.vue ->" + store.state.User.user)
      return store.state.User.user
    });

    return {
      user
    }
  }
}
</script>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  min-height: 100vh;
  background-color: #F3F5FA;

  nav {
    display: flex;
    align-items: center;
    justify-content: space-between;
    padding: 10px 5%;
    background-color: deeppink;
    color: white;

    .navigation__logo {
      font-weight: bold;
      font-size: 24px;
    }

    .navigation__user {
      font-weight: bold;
    }
  }
}
</style>