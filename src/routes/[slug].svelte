<script context="module">
  export async function load({ params, fetch }) {
    const { slug } = params
    //res is response and it will await the response and then return the props which are the page
    const res = await fetch(`/pages/${slug}.json`)
    if (res.ok) {
      const { page } = await res.json()
      return {
        props: { page },
      }
    }
  }
</script>

<script>
  export let page
</script>

<svelte:head>
  <title>Amy Blog</title>
</svelte:head>

<h1 class="text-xl font-semibold mb-5">{page.title}</h1>

<article class="prose">
  {@html page.content.html}
</article>
