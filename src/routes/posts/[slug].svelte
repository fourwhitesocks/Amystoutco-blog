<script context="module">
  export async function load({ params, fetch }) {
    const { slug } = params
    //res is response and it will await the response and then return the props which are the posts
    const res = await fetch(`/posts/${slug}.json`)
    if (res.ok) {
      const { post } = await res.json()
      return {
        props: { post },
      }
    }
  }
</script>

<script>
  export let post

  const {
    title,
    date,
    tags,
    author: { name, authorTitle, picture },
    content: { html },
    coverImage,
    seo: { keywords, description },
  } = post
</script>

<svelte:head>
  <title>Amy Blog</title>
  <!-- trying these below -->
  <meta name="description" content={post.seo.description} />
  <meta name="keywords" content={post.seo.keywords} />
</svelte:head>

<!--  <pre>{JSON.stringify(post, null, 2)}</pre>-->

<div class="sm:-mx-5 md:-mx-10 lg;-mx-20 xl:-mx-38 mb-5 ">
  <img
    src={post.coverImage.url}
    alt={`Cover image for ${title}`}
    class=""
  />
</div>

<h1 class="text-4xl font-semibold mb-5">{title}</h1>

<a href="/" class="inline-flex items-center mb-3">
  <img
    src={picture.url}
    alt={name}
    class="w-12 h-12 rounded-full flex-shrink-0 object-cover object-center"
  />

  <span class="flex-grow.flex.flex-col pl-4">
    <span class="title-font font-medium"> {name}</span>
    <span class="text-secondary.text-xs.tracking-widest">
      {authorTitle}</span
    >
  </span>
</a>

<p class="text-secondary text-xs traking-widest font-semi-bold">
  {new Date(date).toDateString()}
</p>

<div class="mb-5 flex justify-between">
  <div>
    {#if tags}
      <div class="mt-5 space-x-2">
        {#each tags as tag}
          <span class="badge badge-primary">{tag}</span>
        {/each}
      </div>
    {/if}
  </div>
</div>

<article div class="prose">
  {@html html}
</article>
