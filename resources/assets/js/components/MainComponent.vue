<template>
  <div>
    <h2>アップロード画像一覧</h2>
    <image-item
    v-for="image in images"
    v-bind:key="image.id"
    v-bind:image="image"/>
  </div>
</template>
<script>
  export default {
    data() {
      return {
        images: []
      }
    },
    mounted() {
      // コンポーネントが読み込まれるときに実行される。
      // APIからデータを取得してデータに入れる
      axios('/api/').then((response) => {
        this.images = response.data.data
      })
    }
  }
</script>