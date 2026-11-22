<script lang="ts">
  import Exmarkdown from "svelte-exmarkdown";
  import type { Plugin } from "svelte-exmarkdown";

  import rehypeShikiFromHighlighter from "@shikijs/rehype/core";
  import { createHighlighterCoreSync } from "shiki/core";
  import { createJavaScriptRegexEngine } from "shiki/engine/javascript";

  import java from "shiki/langs/java.mjs";
  import theme from "shiki/themes/catppuccin-mocha.mjs";

  const files = import.meta.glob("/src/**/*.md", {
    query: "?raw",
    import: "default",
    eager: true,
  }) as Record<string, string>;

  let { file }: { file: string } = $props();

  function getMarkdown(path: string) {
    path = path.trim();

    if (path.startsWith("$lib/")) {
      path = path.replace("$lib/", "/src/lib/");
    } else if (!path.startsWith("/")) {
      path = `/src/routes/${path}`;
    }

    // Normalize path separators
    path = path.replace(/\\/g, "/").replace(/\/+/g, "/");

    console.log(path);

    return files[path];
  }

  // svelte-ignore state_referenced_locally
  const markdown = getMarkdown(file);

  const highlighter = createHighlighterCoreSync({
    themes: [theme],
    langs: [java],
    engine: createJavaScriptRegexEngine(),
  });

  const shikiPlugin = {
    rehypePlugin: [
      rehypeShikiFromHighlighter,
      highlighter,
      { theme: "catppuccin-mocha" },
    ],
  } satisfies Plugin;
</script>

<div class="markdownContainer">
  {#if markdown}
    <Exmarkdown md={markdown} plugins={[shikiPlugin]} />
  {:else}
    <p>Markdown file not found: {markdown}</p>
  {/if}
</div>

<style>
  .markdownContainer :global(p) {
    margin-block: 0 1rem;
  }

  .markdownContainer :global(h1) {
    margin-block: 1.5rem 0.75rem;
  }

  .markdownContainer :global(h2) {
    margin-block: 1.25rem 0.625rem;
  }

  .markdownContainer :global(h3) {
    margin-block: 1rem 0.5rem;
  }

  .markdownContainer :global(pre) {
    border-radius: 1rem;
    overflow: auto;
    padding: 1rem;
  }

  .markdownContainer {
    background: var(--background-color);
    margin: 5rem;
    border-radius: 1rem;
    padding: 8px;
  }

  .markdownContainer :global(pre) {
    max-height: 50vh;
    overflow: auto;
    padding: 1rem;

    /* Firefox */
    scrollbar-color: #aaa transparent;
  }

  .markdownContainer :global(pre)::-webkit-scrollbar {
    width: 10px;
    height: 10px;
  }

  .markdownContainer :global(pre)::-webkit-scrollbar-track {
    border-radius: 1rem;
    background: transparent;
  }

  .markdownContainer :global(pre)::-webkit-scrollbar-thumb {
    border-radius: 1rem;
    background: #888;
  }

  .markdownContainer :global(pre)::-webkit-scrollbar-thumb:hover {
    background: #666;
  }
</style>
