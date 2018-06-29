<template> 
    <div>
        <h1>画像アップローダー</h1>
    	<h2>画像をアップロードする</h2>
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
            images: []
        }
    },
    mounted() {
        axios.get('/api/').then((response) => {
            this.images = response.data.data
        })
    }
}
</script>