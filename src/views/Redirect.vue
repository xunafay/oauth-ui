<template lang="pug">
  .wrapper
    div(v-if="state === 'success'")
      img(src="https://cdn.betterttv.net/emote/5f5056523769246c0320ee09/3x")
      span All done chief, you can close this tab now
    div(v-if="state === 'pending'")
      img(src="https://cdn.discordapp.com/emojis/679829173560147984.gif?v=1")
      span Patching you into the mainframe
    div(v-if="state === 'error'")
      img(src="https://cdn.discordapp.com/emojis/759522874645282848.png?v=1")
      span Something went wrong
</template>

<script lang="ts">
import Vue from 'vue';
import Axios from 'axios';

export default Vue.extend({
  name: 'redirect',
  data: () => ({
    state: 'pending',
  }),
  mounted() {
    const { code } = this.$route.query;
    if (code) {
      Axios.request({
        method: 'POST',
        url: `${process.env.VUE_APP_API}twitch`,
        data: { code },
      })
        .then(() => this.state = 'success')
        .catch(() => this.state = 'error');
    } else {
      this.state = 'error';
    }
  },
});
</script>

<style lang="scss" scoped>
.wrapper {
  display: flex;
  height: 100%;
  justify-content: center;
  align-items: center;

  div {
    display: flex;
    align-items: center;
  }

  img {
    height: 32px;
    margin-right: 12px;
  }
}
</style>
