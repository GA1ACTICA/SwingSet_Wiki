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
  <div class="nav-slot" class:collapsed={!currentPath.includes("/wiki")}>
    {#if currentPath.includes("/wiki")}
      <div
        in:fly={{ x: -250, duration: 500 }}
        out:fly={{ x: -250, duration: 500 }}
      >
        <Nav />
      </div>
    {/if}
  </div>

  <div class="page-container">
    {#key page.url.href}
      <section
        class:javadoc={currentPath.includes("/javadoc")}
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
  }

  .nav-slot {
    flex: 0 0
      max(
        15vw,
        clamp(var(--nav-min-width), var(--nav-width), var(--nav-max-width))
      );
    overflow: hidden;
    transition: flex-basis 500ms ease;
  }

  .nav-slot.collapsed {
    flex-basis: 0;
  }

  .page-container {
    display: grid;
    flex: 1;
    min-width: 0;
    min-height: 0;
  }

  section {
    grid-area: 1 / 1;
    padding: 3rem;
    width: 100%;
    box-sizing: border-box;
    min-width: 0;
  }

  section.javadoc {
    padding: 0;
    max-width: none;
    height: 90vh;
  }

  section.javadoc :global(iframe) {
    display: block;
    width: 100%;
    height: 100%;
    border: none;
  }
</style>
