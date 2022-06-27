<template>
  <div>
    <h1>Hellohere are my sushis</h1>
    <div v-for="sushi of sushis" :key="sushi.id">
      <NuxtLink :to="'/sushis/' + sushi.id">
        <h2>{{ sushi.title }}</h2>
        <img :src="sushi.image">
      </NuxtLink>
    </div>
  </div>
</template>

<script>
export default {
  name: 'SushiPage',
  data () {
    return {
      sushis: []
    }
  },
  // eslint-disable-next-line require-await
  async fetch () {
    // eslint-disable-next-line no-console
    this.sushis = await fetch(
      'https://www.wawasensei.dev/api/demo-nuxt/getSushis'
    )
      .then((res) => {
        return res.json()
      })
      .then(response => response.Table)
  },
  head: {
    title: 'mes sushis ',
    meta: [
      { charset: 'utf-8' },
      { name: 'viewport', content: 'width=device-width, initial-scale=1' },
      {
        hid: 'description',
        name: 'description',
        content: 'ma description de site web'
      }
    ],
    link: [{ rel: 'icon', type: 'image/x-icon', href: '/favicon.ico' }]
  }
}
</script>
