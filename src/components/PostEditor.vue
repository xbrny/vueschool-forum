<template>
  <form @submit.prevent="addPost">
    <div class="form-group">
      <textarea
      v-model="text"
      cols="30"
      rows="10"
      class="form-input">
    </textarea>
  </div>
  <div class="btn-group">
    <button type="submit" class="btn btn-blue">Submit</button>
  </div>
</form>
</template>

<script>
export default {
  props: {
    threadId: {
      required: true
    }
  },

  data () {
    return {
      text: ''
    }
  },

  methods: {
    addPost () {
      const postId = 'NewPostWithId' + Math.random()
      const post = {
        '.key': postId,
        publishedAt: Date.now(),
        text: this.text,
        userId: 'ALXhxjwgY9PinwNGHpfai6OWyDu2',
        threadId: this.threadId
      }
      this.$emit('save', {post})
      this.text = ''
    }
  }
}
</script>