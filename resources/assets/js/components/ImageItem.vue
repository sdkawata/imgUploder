<template>
  <el-col v-bind:span="12">
    <el-card>
    　　<img v-bind:src="image.file_url" width="100%"><br>
    　　コメント：{{image.comment}}<br>
    　　作成日：{{image.created_at.date}}<br>
    　　更新日：{{image.updated_at.date}}<br>
    　　<el-button v-if="!commentEditing" @click="commentEditing=true" round>編集</el-button>
	　　<template v-else>
 	　　　 <el-input v-model="comment" type="text"/><br>
      <el-button @click="editComment" round type="success">変更確定</el-button>
	　　</template>
	　　<el-button type="danger" v-on:click="$emit('delete')">削除</el-button>
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