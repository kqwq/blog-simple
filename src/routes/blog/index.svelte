<script context="module">
  const allPosts = import.meta.glob("./*.{md,svx}")
  
  let body = []
  for (let path in allPosts) {
    body.push(
      allPosts[path]().then(({ metadata }) => {
        return { path, metadata }
      })
    )
  }

  export const load = async() => {
    const posts = await Promise.all(body)
    
    return {
      props: {
        posts
      }
    }
  }


</script>
<script>
import { linkPath } from "$lib/LinkPath.svelte";

export let posts
</script>

<h1>Blog</h1>
<ul>
  {#each posts as {path, metadata: {title, tags}}}
    <li>
      <a href="/blog/{linkPath(path)}">{title}</a>
      <p>
        {#each (tags||[]) as tag}
          <p><a class="tag" href={`/tags/${tag}`}>#{tag}</a></p>
        {/each}
      </p>
    </li>
  {/each}
</ul>

<style>
  ul {
    margin: 0;
    font-size: 0.8rem;
  }
  li {
    margin-bottom: 20px;
  }
  .tag {
    text-decoration: none;
    margin-right: 10px;
    color: #555;
  }
  .tag:hover {
    color: blue;
  }
</style>