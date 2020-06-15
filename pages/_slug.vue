<template>
  <section class="section">
    <div class="container">
      <div class="columns">
        <div class="column is-three-fifths is-offset-one-fifth">
          <h1 class="title is-1 has-text-centered">
            {{ post.title }}
          </h1>

          <nuxt-content :document="post" />

          <div class="mt-4 has-text-centered">
            <nuxt-link class="button is-primary is-light" to="/">
              View All Posts
            </nuxt-link>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script>
export default {
  async asyncData ({ $content, params }) {
    const post = await $content('posts', params.slug).fetch()

    return { post }
  },
  head () {
    return {
      title: this.post.title,
      meta: [
        { hid: 'description', name: 'description', content: this.post.description },
        { hid: 'og:title', property: 'og:title', content: this.post.title },
        { hid: 'og:description', property: 'og:description', content: this.post.description },
        { hid: 'twitter:title', name: 'twitter:title', content: this.post.title },
        { hid: 'twitter:description', name: 'twitter:description', content: this.post.description }
      ]
    }
  }
}
</script>

<style>
  .nuxt-content h2 {
    font-size: 1.25rem;
    font-weight: 600;
    line-height: 1.125;
    margin-top: 1.5rem;
    margin-bottom: 1.5rem;
  }

  .nuxt-content h2 > a::before {
    content: "#";
  }

  .nuxt-content h2 a .icon {
    height: 0.5rem;
    width: 0.5rem;
  }
</style>
