<template>
  <div>
    <div class="col-large push-top">

      <h1>{{thread.title}}</h1>

      <p>
        By <a href="#" class="link-unstyled">{{users[thread.userId].name}}</a>, 2 hours ago.
        <span style="float:right; margin-top: 2px;" class="hide-mobile text-faded text-small">3 replies by 3 contributors</span>
      </p>

      <PostList :posts="posts"/>

      <form @submit.prevent="addPost">
        <div class="form-group">
          <textarea
            v-model="newPostText"
            cols="30"
            rows="10"
            class="form-input">
          </textarea>
        </div>
        <div class="btn-group">
          <button type="submit" class="btn btn-blue">Submit</button>
        </div>
      </form>

    </div>
  </div>
</template>

<script>
import sourceData from '@/data'
import PostList from '@/components/PostList'
export default {
  components: {
    PostList
  },

  props: {
    id: {
      required: true,
      type: String
    }
  },

  data () {
    return {
      thread: sourceData.threads[this.id],
      users: sourceData.users,
      newPostText: ''
    }
  },

  computed: {
    posts () {
      const postsId = Object.values(this.thread.posts)
      return Object.values(sourceData.posts).filter((post) => postsId.includes(post['.key']))
    }
  },

  methods: {
    addPost () {
      const postId = 'NewPostWithId' + Math.random()
      const post = {
        '.key': postId,
        publishedAt: Date.now(),
        text: this.newPostText,
        userId: 'ALXhxjwgY9PinwNGHpfai6OWyDu2',
        threadId: this.id
      }
      this.$set(sourceData.posts, postId, post)
      this.$set(this.thread.posts, postId, postId)
      this.$set(this.users[post.userId].posts, postId, postId)
      this.newPostText = ''
    }
  }
}
</script>
