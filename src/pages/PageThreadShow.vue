<template>
  <div>
    <div class="col-large push-top">

      <h1>{{thread.title}}</h1>

      <p>
        By <a href="#" class="link-unstyled">{{users[thread.userId].name}}</a>, 2 hours ago.
        <span style="float:right; margin-top: 2px;" class="hide-mobile text-faded text-small">3 replies by 3 contributors</span>
      </p>

      <PostList :posts="posts"/>

      <PostEditor
        @save="addPost"
        :threadId="thread['.key']"
      />

    </div>
  </div>
</template>

<script>
import sourceData from '@/data'
import PostList from '@/components/PostList'
import PostEditor from '@/components/PostEditor'
export default {
  components: {
    PostList,
    PostEditor
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
      users: sourceData.users
    }
  },

  computed: {
    posts () {
      const postsId = Object.values(this.thread.posts)
      return Object.values(sourceData.posts).filter((post) => postsId.includes(post['.key']))
    }
  },

  methods: {
    addPost ({post}) {
      const postId = post['.key']
      this.$set(sourceData.posts, postId, post)
      this.$set(this.thread.posts, postId, postId)
      this.$set(this.users[post.userId].posts, postId, postId)
      console.log(post)
    }
  }
}
</script>
