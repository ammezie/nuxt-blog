<template>
  <div>
    <section class="hero is-primary has-text-centered">
      <div class="hero-body">
        <div class="container">
          <h1 class="title">
            Tech Blog
          </h1>
          <h2 class="subtitle">
            An awesome tech blog
          </h2>
        </div>
      </div>
    </section>

    <section class="section">
      <div class="container">
        <div class="columns">
          <div class="column is-three-fifths is-offset-one-fifth">
            <div v-for="post in posts" :key="post.slug" class="mb-5">
              <h3 class="title is-4">
                <nuxt-link :to="post.slug">
                  {{ post.title }}
                </nuxt-link>
              </h3>
              <div>
                {{ post.description }}
              </div>
            </div>
          </div>
        </div>
      </div>
    </section>
  </div>
</template>

<script>
export default {
  async asyncData ({ $content }) {
    const posts = await $content('posts').sortBy('createdAt', 'desc').fetch()

    return { posts }
  }
}
</script>

<style>
  h3 a {
    color: #363636;
  }

  h3 a:hover {
    color: #3273dc;
  }
</style>
