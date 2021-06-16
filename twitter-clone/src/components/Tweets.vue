<template>
  <div class="tweet-item" @click="favouriteTweet(tweet.id)">
    <div class="user-profile-tweet">
      <div class="user-tweet">@{{ username }}</div>
      <div class="tweet-content">
        {{ tweet.content }}
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "Tweets",
  props: {
    username: String,
    tweet: Object,
  },

  methods: {
    favouriteTweet(id) {
      this.$emit("favourite", id);
    },
  },
};
</script>

<style scoped>
.tweet-item {
  padding: 20px;
  background: #fff;
  border: 1px solid rgb(13, 58, 88);
  box-sizing: border-box;
  cursor: pointer;
  transition: all 0.25s ease;
  display: flex;
}
.tweet-item:hover {
  transform: scale(1.1, 1.1);
}
.tweet-content {
  margin: 5px 5px;
}
</style>
