<template>
  <div class="userProfile">
    <div class="userDetails">
      <strong>
        <h1>@{{ state.user.username }}</h1>
      </strong>

      <div class="userBadge" v-if="state.user.isAdmin">Admin</div>
      <div id="followersBadge">Followers:{{ state.followers }}</div>

      <form
        action
        class="newTweet"
        @submit.prevent="submitTweet()"
        :class="{ exceeded: newTweetXterCount > 180 }"
      >
        <label for="newtweet">
          <strong>New Tweet</strong>
          ({{ newTweetXterCount }}/180)
        </label>
        <textarea
          name
          id="newtweet"
          cols="30"
          rows="5"
          v-model="state.newTweetContent"
        ></textarea>

        <div class="createTweetType">
          <label for="tweetType">Type:</label>
          <select name id="tweetType" v-model="state.selectedTweetType">
            <option
              :value="option.value"
              v-for="(option, index) in state.tweetTypes"
              :key="index"
              >{{ option.name }}</option
            >
          </select>
        </div>

        <button>Tweet</button>
      </form>
      <router-link to="/">
        <button id="back2home">Bak to Home</button>
      </router-link>
    </div>

    <div class="userProfileTweets">
      <Tweets
        v-for="tweet in state.user.tweets"
        :key="tweet.id"
        :username="state.user.username"
        :tweet="tweet"
        @favourite="toggleFavourite"
      />
    </div>
  </div>
</template>

<script>
import { computed, reactive, onMounted } from "vue";
import { useRoute } from "vue-router";
import Tweets from "../components/Tweets";
import { users } from "../assets/users";

export default {
  name: "UserProfile",
  components: {
    Tweets,
  },

  setup() {
    const route = useRoute();
    const userId = computed(() => route.params.userId);

    const state = reactive({
      newTweetContent: "",
      selectedTweetType: "instant",
      tweetTypes: [
        { value: "draft", name: " Draft Tweets" },
        { value: "instant", name: "Instant Tweets" },
      ],
      followers: 0,
      user: users[userId.value - 1] || users[0],
    });

    const newTweetXterCount = computed(() => state.newTweetContent.length);

    function followUser() {
      state.followers++;
    }

    function toggleFavourite(id) {
      console.log(`favourite tweeet ${id}`);
    }

    function submitTweet() {
      if (state.newTweetContent && state.selectedTweetType !== "draft") {
        state.user.tweets.unshift({
          id: state.user.tweets.length + 1,
          content: state.newTweetContent,
        });

        state.newTweetContent = "";
      }
    }

    onMounted(followUser);

    return {
      state,
      submitTweet,
      toggleFavourite,
      followUser,
      newTweetXterCount,
      onMounted,
      route,
      userId,
    };
  },

  watch: {
    followers(newFollowerCount, oldFollowerCount) {
      if (oldFollowerCount < newFollowerCount) {
        console.log(`${this.user.userName} has gained a new follower!`);
      }
    },
  },
};
</script>

<style scoped>
.userProfile {
  color: rgb(12, 12, 12);
  display: flex;
  padding-left: 5rem;
}
.userDetails {
  background: rgb(200, 210, 218);
  padding: 20px 20px;
  width: 250px;
  flex-direction: column;
}
.exceeded {
  color: red;
  border-color: red;
}
#followersBadge {
  font-size: 12px;
  padding-right: 145px;
  margin-top: 5px;
}
.newTweet {
  display: flex;
  flex-direction: column;
  padding-top: 20px;
}
textarea {
  border-color: royalblue;
}
.userBadge {
  background: rgb(36, 137, 219);
  width: 45px;
  padding: 5px 10px;
  margin-left: 1.4rem;
  border-radius: 4px;
}
h1 {
  font-size: 1.6rem;
}
.userProfileTweets {
  flex-direction: column;
  justify-content: start;
  align-items: flex-start;
  flex-grow: 3;
  margin: 0 50px;
}
.createTweetType {
  margin: 20px 10px;
  text-align: left;
}

button {
  cursor: pointer;
}

#back2home {
  margin-top: 30px;
  border-radius: 15px;
}
</style>
