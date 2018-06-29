<template> 
    <div>
        <h1>画像アップローダー</h1>
    	<h2>画像をアップロードする</h2>
        画像ファイル：<input type="file" ref="file">
        コメント：<input type="text" v-model="comment">
        <button type="submit" v-on:click="uploadImage">アップロード</button>
        <h2>アップロード画像一覧</h2>
        <div>
        <div v-for="image in images" style="margin: 10px;border: 1px solid;width:50%;">
            <img v-bind:src="image.file_url" style="width:100%"><br>
            コメント：{{image.comment}}<br>
            作成日：{{image.created_at.date}}<br>
            更新日：{{image.updated_at.date}}<br>
        </div>
        </div>
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
    mounted() {
        axios.get('/api/').then((response) => {
            this.images = response.data.data
        })
    },
    methods: {
      uploadImage() {
      	let formData = new FormData()
      	formData.append('file', this.$refs.file.files[0])
      	formData.append('comment', this.comment)
      	axios.post('/api/', formData).then((response) => {
        this.images.unshift(response.data.data)
      	})
      }
    },
}
</script>