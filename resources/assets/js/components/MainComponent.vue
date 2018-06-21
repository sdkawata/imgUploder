<template>
  <div>
    <h2>アップロード画像一覧</h2>
    <div v-for="image in images" style="margin: 10px;border: 1px solid;width:50%;">
      <img v-bind:src="image.file_url" width="100%"><br>
      コメント：{{image.comment}}<br>
      作成日：{{image.created_at.date}}<br>
      更新日：{{image.updated_at.date}}<br>
      <a>編集</a>
      <button type="submit">削除</button>
    </div>
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