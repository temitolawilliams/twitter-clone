<template>
  <div class="home">
    <h1>Twitter Clone</h1>
    <div class="user-name-list">
      <router-link
        v-for="user in users"
        :key="user.userId"
        :to="{ name: 'UserProfile', params: { userId: user.id } }"
      >
        {{ user.username }}
      </router-link>
    </div>
  </div>
</template>

<script>
// @ is an alias to /src
import { users } from "../assets/users";

export default {
  name: "Home",
  setup() {
    return {
      users,
    };
  },
};
</script>

<style scoped>
h1 {
  border: 2px solid black;
  text-align: center;
  background: black;
  color: aliceblue;
}
.home {
  padding: 50px 5%;
}
.user-name-list {
  display: flex;
  flex-direction: column;
  line-height: 50px;
  font-size: 1.6rem;
  font-weight: bolder;
}
</style>
