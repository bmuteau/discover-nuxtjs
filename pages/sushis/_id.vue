/* eslint-disable vue/no-multiple-template-root */
<template>
  <div>
    <h1>{{ sushi.title }}</h1>
    <p>{{ sushi.description }}</p>
    <img :src="sushi.image">
  </div>
</template>

<script>
export default {
  // eslint-disable-next-line require-await
  async asyncData ({ params }) {
    // eslint-disable-next-line no-console
    console.log(params)
    // eslint-disable-next-line no-console
    const sushis = await fetch(`https://www.wawasensei.dev/api/demo-nuxt/getSushi?id=${params.id}`)
      .then((res) => {
        return res.json()
      }).then(response => response.Table)
    if (sushis && sushis.length) {
      return {
        sushi: sushis[0]
      }
    } else {
      return {
        sushi: {
          title: " Je n'existe pas",
          description: 'Je suis une 404',
          image: ''
        }
      }
    }
  },
  head () {
    return {
      title: this.sushi.title
    }
  },
  watch: {
    '$route.query': '$fetch'
  }

}
</script>
