<template lang="pug">
.wrapper
  .card
    .icons
      img(src="https://cdn.discordapp.com/avatars/168706817348730881/2a4ac8123c6b332fc6014c539110c4b1.png?size=128")
      IconifyIcon(:icon="icons.twitchIcon" :style="{color: '#9147ff', fontSize: '24px', paddingLeft: '4px'}")
    .text
      span.bold Xunafay
      span requires access
      span to your
      span.bold.purple twitch
    button(@click="register") Authorize
  .gundma
    img(src="https://cdn.discordapp.com/emojis/727651864094572546.png?v=1")
    span you
    span.bbold  will
    span  give access
</template>

<script lang="ts">
import Vue from 'vue';
import IconifyIcon from '@iconify/vue';
import twitchIcon from '@iconify/icons-simple-icons/twitch';

export default Vue.extend({
  name: 'Home',
  components: {
    IconifyIcon,
  },
  data: () => ({
    icons: {
      twitchIcon,
    },
    scopes: ['clips:edit'],
  }),
  methods: {
    register() {
      window.location.href = `https://id.twitch.tv/oauth2/authorize?client_id=${process.env.VUE_APP_CLIENT_ID}&redirect_uri=${process.env.VUE_APP_REDIRECT_URI}&response_type=code&scope=${this.scopes.join(' ')}&force_verify=true`;
    },
  },
});
</script>

<style lang="scss" scoped>
.wrapper {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  height: 100%;

  .card {
    padding: 22px;
    border-radius: 32px;
    box-shadow: 18px 18px 30px #D1D9E6, -18px -18px 30px #FFFFFF;
    display: flex;
    flex-direction: row;
    position: relative;

    .icons {
      display: flex;
      flex-direction: column;
      justify-content: space-between;

      img {
        width: 32px;
        height: 32px;
        border-radius: 50%;
      }
    }

    .text {
      display: flex;
      flex-direction: column;
      margin-left: 10px;
      margin-top: 6px;
      margin-right: 96px;
    }

    button {
      display: flex;
      flex-direction: row;
      justify-content: center;
      align-items: center;
      padding: 12px 28px;

      background: #9147FF;
      border-radius: 32px 0px;

      position: absolute;
      bottom: 0;
      right: 0;
    }
  }

  .gundma {
    display: flex;
    align-items: center;
    margin-top: 5vh;

    .bbold {
      padding: 0px 4px;
    }

    img {
      width: 32px;
    }
  }
}
</style>
