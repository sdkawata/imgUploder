<template>
  <el-col v-bind:span="12">
    <el-card>
    　　<img v-bind:src="image.file_url" width="100%"><br>
    　　コメント：{{image.comment}}<br>
    　　作成日：{{image.created_at.date}}<br>
    　　更新日：{{image.updated_at.date}}<br>
    　　<a v-if="!commentEditing" @click="commentEditing=true">編集</a>
	　　<template v-else>
 	　　　 <input v-model="comment" type="text"><br>
    　　 <button @click="editComment">変更確定</button>
	　　</template>
	　　<button type="submit" v-on:click="$emit('delete')">削除</button>
    </el-card>
  </el-col>
</template>
<script>
export default {
  props: ['image'],
  data() {
    return {
    	commentEditing: false,
    	comment: ''
    }
  },
  methods: {
     editComment() {
      this.$emit('edit', {id: this.image.id, comment: this.comment})
      this.commentEditing=false
    }
  }
}
</script>