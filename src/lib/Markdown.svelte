<script lang="ts">
  import Exmarkdown from "svelte-exmarkdown";
  import type { Plugin } from "svelte-exmarkdown";

  import rehypeShikiFromHighlighter from "@shikijs/rehype/core";
  import { createHighlighterCoreSync } from "shiki/core";
  import { createJavaScriptRegexEngine } from "shiki/engine/javascript";

  import java from "shiki/langs/java.mjs";
  import theme from "shiki/themes/catppuccin-mocha.mjs";

  const files = import.meta.glob("/src/lib/**/*.md", {
    query: "?raw",
    import: "default",
    eager: true,
  }) as Record<string, string>;

  let { file }: { file: string } = $props();

  function getMarkdown(path: string) {
    if (path.startsWith("$lib/")) {
      path = path.replace("$lib/", "/src/lib/");
    }

    if (!path.startsWith("/")) {
      path = `/src/lib/${path}`;
    }

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
    <p>Markdown file not found: {file}</p>
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
</style>
