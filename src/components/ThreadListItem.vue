<template>
  <div class="thread">
    <div>
      <p>
        <router-link :to="{ name: 'PageThreadShow', params: { id: thread['.key'] } }">
          {{thread.title}}
        </router-link>
      </p>
      <p class="text-faded text-xsmall">
        By <a href="#">{{user.name}}</a>, {{thread.publishedAt}}
      </p>
    </div>

    <div class="activity">
      <p class="replies-count">
        {{postsCount}} <template v-if="postsCount > 1">Replies</template><template v-else>Reply</template>
      </p>
    </div>
  </div>
</template>

<script>
import sourceData from '@/data'
export default {
  props: {
    thread: {
      required: true,
      type: Object
    }
  },
  data () {
    return {
      users: sourceData.users
    }
  },
  computed: {
    postsCount () {
      return Object.keys(this.thread.posts).length
    },
    user () {
      return sourceData.users[this.thread.userId]
    }
  }
}
</script>