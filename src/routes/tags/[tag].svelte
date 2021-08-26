<script context="module">
  const allPosts = import.meta.glob("../blog/*.{md,svx}")
  
  let body = []
  for (let path in allPosts) {
    body.push(
      allPosts[path]().then(({ metadata }) => {
        return { path, metadata }
      })
    )
  }

  export const load = async({page}) => {
    const posts = await Promise.all(body)
    const tag = page.params.tag

    const filteredPosts = posts.filter((post) => {
      return post.metadata.tags?.includes(tag)
    })
    
    return {
      props: {
        filteredPosts,
        tag
      }
    }
  }


</script>

<script>
  import { linkPath } from "$lib/LinkPath.svelte";
  export let filteredPosts
  export let tag
</script>

<h1>#{tag}</h1>
<p>This tag appears in</p>
<ul>
{#each filteredPosts as fp}
  <li><a href={linkPath(fp.path)}>{fp.metadata.title}</a></li>
{/each}
</ul>

{JSON.stringify(filteredPosts)}