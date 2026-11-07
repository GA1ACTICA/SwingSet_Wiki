<script>
  import favicon from "$lib/assets/favicon.svg";
  import Nav from "$lib/Nav.svelte";
  import Header from "$lib/Header.svelte";
  import "$lib/global.css";
  import { page } from "$app/state";

  let { children } = $props();
</script>

<svelte:head>
  <link rel="icon" href={favicon} />
</svelte:head>

<Header />
<div>
  {#if page.url.pathname.startsWith("/wiki")}
    <Nav />
  {/if}
  <section>{@render children()}</section>
</div>

<style>
  div {
    display: flex;
  }

  section {
    padding: 3rem;
    max-width: 70%;
  }
</style>
