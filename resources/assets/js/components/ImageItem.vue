<template>
  <div style="margin: 10px;border: 1px solid;width:50%;">
    <img v-bind:src="image.file_url" width="100%"><br>
    コメント：{{image.comment}}<br>
    作成日：{{image.created_at.date}}<br>
    更新日：{{image.updated_at.date}}<br>
    <a v-if="!commentEditing" @click="commentEditing=true">編集</a>
	<template v-else>
 	 <input ref="comment" type="text"><br>
     <button @click="editComment">変更確定</button>
	</template>
    <button type="submit">削除</button>
  </div>
</template>
<script>
export default {
  props: ['image'],
  data() {
    return {
    	commentEditing: false
    }
  },
  methods: {
     editComment() {
      this.$emit('edit', {id: this.image.id, comment: this.$refs.comment.value})
      this.commentEditing=false
    }
  }
}
</script>