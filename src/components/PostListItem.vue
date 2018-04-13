<template>
  <div class="post">
    <div class="user-info">
      <a href="profile.html#profile-details" class="user-name">{{user.name}}</a>

      <a href="profile.html#profile-details">
        <img class="avatar-large" :src="user.avatar" alt="">
      </a>

      <p class="desktop-only text-small">{{postsByUserCount}} posts</p>

    </div>

    <div class="post-content">
      <div>
        {{post.text}}
      </div>
    </div>

    <div class="post-date text-faded">
      {{post.publishedAt | formattedDateString}}
    </div>
  </div>
</template>

<script>
import sourceData from '@/data'
import fecha from 'fecha'
export default {
  props: {
    post: {
      required: true,
      type: Object
    }
  },

  filters: {
    formattedDateString (date) {
      return fecha.format(date, 'dddd MMMM Do, YYYY')
    }
  },

  computed: {
    user () {
      return sourceData.users[this.post.userId]
    },
    postsByUserCount () {
      return Object.keys(this.user.posts).length
    }
  }
}
</script>