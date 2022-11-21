<template>
  <div>
    <v-list-item v-for="music in musicInfo">
      <v-list-item-avatar>
        <v-img :src="music.snippet.thumbnails.default.url" />
      </v-list-item-avatar>

      <v-list-item-content>
        <v-list-item-title v-text="music.snippet.title"></v-list-item-title>

        <v-list-item-subtitle
          v-text="music.snippet.description"
        ></v-list-item-subtitle>
      </v-list-item-content>

      <v-list-item-action>
        <v-btn icon @click="playMusic()">
          <v-icon color="grey lighten-1">mdi-arrow-right-drop-circle</v-icon>
        </v-btn>
      </v-list-item-action>
    </v-list-item>
  </div>
</template>

<script>
import axios from "axios";

export default {
  data() {
    return {
      musicInfo: null,
      apiKey: "AIzaSyDtxot_xW8r-kKs7Cce7KvdnpuRB99REXM",
      keyWord: "music",
      maxResults: 10,
    };
  },
  methods: {
    playMusic() {
      var music = this.musicInfo;
      var link = music.map(
        (music) => `https://www.youtube.com/watch?v=${music.id.videoId}`
      );
      console.log(link);
    },
  },
  mounted() {
    axios
      .get(
        `https://youtube.googleapis.com/youtube/v3/search?part=snippet&maxResults=${this.maxResults}&q=${this.keyWord}&key=${this.apiKey}`
      )
      .then((result) => {
        this.musicInfo = result.data.items;
      })
      .catch((error) => console.log(error));
  },
};
</script>

<style lang="scss" scoped></style>
