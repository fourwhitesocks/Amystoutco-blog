<script context="module">

  export const load = async ({ fetch }) => {

    const res = await fetch('/posts.json')
    if (res.ok) {
      const { posts } = await res.json()
      return { 
        props: { posts } ,
      }
    }
  }

</script>

<!--for the json stringify test see 29:31 mins in!!-->
<script>
  export let posts
</script>

<!--<pre>{JSON.stringify(posts, null, 2)}</pre> shows how you get the exact same thing as if you went to the posts.json -->




<h1>Welcome to SvelteKit</h1>
<p>
  Visit <a href="https://kit.svelte.dev">kit.svelte.dev</a> to read the
  documentation
</p>

<p>stopped at 30:05 in</p>
