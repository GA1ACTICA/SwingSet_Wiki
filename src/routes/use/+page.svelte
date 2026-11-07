<script>
  import Markdown from "$lib/Markdown.svelte";
</script>

<section>
  <article>
    <div class="scrollable"><Markdown file="$lib/test.md" /></div>
  </article>
</section>

<style>
  .scrollable {
    background: var(--background-color);
    margin: 5rem;
    border-radius: 1rem;
    padding: 8px;
  }

  div :global(pre) {
    height: 50vh;
    overflow: auto;
    padding: 1rem;

    /* Firefox */
    scrollbar-color: #aaa transparent;
  }

  div :global(pre)::-webkit-scrollbar {
    width: 10px;
    height: 10px;
  }

  div :global(pre)::-webkit-scrollbar-track {
    border-radius: 1rem;
    background: transparent;
  }

  div :global(pre)::-webkit-scrollbar-thumb {
    border-radius: 1rem;
    background: #888;
  }

  div :global(pre)::-webkit-scrollbar-thumb:hover {
    background: #666;
  }
</style>
