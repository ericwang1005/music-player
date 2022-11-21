<template>
  <v-list>
    <music />
  </v-list>
</template>

<script>
export default {
  components: {
    music: require("@/components/Music.vue").default,
  },
};
</script>

<style lang="scss" scoped></style>
