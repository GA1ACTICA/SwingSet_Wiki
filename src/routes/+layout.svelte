<script>
  import favicon from "$lib/assets/favicon.svg";
  import Nav from "$lib/Nav.svelte";
  import Header from "$lib/Header.svelte";
  import "$lib/global.css";
  import { page } from "$app/state";
  import { fade, fly } from "svelte/transition";

  let { children } = $props();
  let currentPath = $derived(page.url.pathname);
</script>

<svelte:head>
  <link rel="icon" href={favicon} />
</svelte:head>

<Header />

<div class="layout">
  <div class="nav-slot">
    {#if currentPath.includes("/wiki")}
      <div
        in:fly={{ x: -250, duration: 500, delay: 400 }}
        out:fly={{ x: -250, duration: 500, delay: 400 }}
      >
        <Nav />
      </div>
    {/if}
  </div>

  <div class="page-container">
    {#key page.url.href}
      <section
        in:fade={{ duration: 400, delay: 400 }}
        out:fade={{ duration: 400 }}
      >
        {@render children()}
      </section>
    {/key}
  </div>
</div>

<style>
  .layout {
    display: flex;
    align-items: flex-start;
  }

  .nav-slot {
    flex: 0 0 15rem;
  }

  .page-container {
    display: grid;
    flex: 1;
    min-width: 0;
  }

  section {
    grid-area: 1 / 1;
    padding: 3rem;
    max-width: 70%;
    width: 100%;
    box-sizing: border-box;
  }
</style>
