<template>
  <div>
    <h2>アップロード画像一覧</h2>
    <h1>画像アップローダー</h1>
    <h2>画像をアップロードする</h2>
	<el-upload
	ref="upload"
	action=""
	:limit="1"
	:auto-upload="false">
	  <el-button slot="trigger" size="small" type="primary">
	    クリックしてファイルをアップロード
	  </el-button>
	</el-upload><br>
	コメント<el-input v-model="comment"/>
	<el-button type="success" @click="uploadImage">アップロード</el-button>
	
	<el-row type="flex" style="flex-wrap:wrap;">
    <image-item
    v-for="image in images"
    v-bind:key="image.id"
    v-bind:image="image"
    v-on:delete="deleteImage(image.id)"
    v-on:edit="editComment"/>
    </el-row>
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
	   formData.append('file', this.$refs.upload.uploadFiles[0].raw)
	   this.$refs.upload.clearFiles()
	   formData.append('comment', this.comment)
	   axios.post('/api/', formData).then((response) => {
	     this.images.unshift(response.data)
	   })
	  },
	  editComment({id, comment}) {
	    axios.put(`/api/${id}`, {comment}).then((response) => {
	      let index = this.images.findIndex((image) => image.id === id)
	      this.$set(this.images, index, response.data.data)
	    })
	  },
      deleteImage(id) {
        axios.delete(`/api/${id}`).then((response) => {
          this.images = this.images.filter((image) => image.id !== id);
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