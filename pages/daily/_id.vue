<template>
  <section>
    netlifyデプロイテスト
    {{ entry }}
  </section>
</template>

<script>
export default {
  // store
  // computed: {
  //   // stateの情報を取得
  //   ApiFlag () { return this.$store.state.daily.ApiFlag },
  //   article () { return this.$store.state.daily.article }
  // },
  data() {
    return {
      entry: ''
    };
  },
  async asyncData({ route, app, store, payload }) {
    if (payload) return payload;
    // console.log(store.state.daily.ApiFlag)
  }
}
</script>
