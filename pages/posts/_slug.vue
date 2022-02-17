<template>
  <div>
    <h1>{{ title }}</h1>
    <p>{{ body }}</p>
    <p>post: {{ id }}</p>
    <p> comment : {{ comment }}</p>
    <NuxtLink :to="`/posts/${id + 1}`">
      suivant
    </NuxtLink>
  </div>
</template>

<script>
export default {
  async asyncData ({ params, $axios }) {
    const slug = params.slug

    const { title, body, id } = await $axios.$get(`https://jsonplaceholder.typicode.com/posts/${slug}`)

    const res = await $axios.get(`https://jsonplaceholder.typicode.com/posts/${slug}/comments`)

    console.log(res)

    const comment = res.data[0].body

    return { title, body, id, slug, comment }
  }
}
</script>
