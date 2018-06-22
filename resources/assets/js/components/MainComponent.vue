<template>
  <div>
    <h2>アップロード画像一覧</h2>
    <h1>画像アップローダー</h1>
    <h2>画像をアップロードする</h2>
    画像ファイル<input type="file" ref="file"><br>
    コメント<input type="text" v-model="comment"><br>
    <button type="submit" v-on:click="uploadImage">アップロード</button>
    <image-item
    v-for="image in images"
    v-bind:key="image.id"
    v-bind:image="image"
    v-on:edit="editComment"/>
  </div>
</template>
<script>
  export default {
    data() {
      return {
        images: [],
        comment: ''
      }
    },
  	methods: {
      uploadImage() {
      	let formData = new FormData()
      	formData.append('file', this.$refs.file.files[0])
      	formData.append('comment', this.comment)
      	axios.post('/api/', formData).then((response) => {
        this.images.push(response.data.data)
      	})
      },
	  editComment({id, comment}) {
	    axios.put(`/api/${id}`, {comment}).then((response) => {
	      let index = this.images.findIndex((image) => image.id === id)
	      this.$set(this.images, index, response.data.data)
	    })
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