<script>
  import { page } from "$app/state";
  import Dropdown from "./Dropdown.svelte";
</script>

<nav>
  <ul>
    <li>
      <a
        href="/wiki/introduction"
        class:active={page.url.pathname.includes("/introduction")}
        >Introduction</a
      >
    </li>
    <hr />

    <Dropdown
      title="Game guides"
      open={page.url.pathname.includes("/creating_a_game")}
    >
      {#snippet children()}
        <li>
          <a
            class:active={page.url.pathname.includes("/setup")}
            href="/wiki/creating_a_game/setup">Setup</a
          >
        </li>
        <li>
          <a
            class:active={page.url.pathname.includes("/rules")}
            href="/wiki/creating_a_game/rules">Game rules</a
          >
        </li>
        <li>
          <a
            class:active={page.url.pathname.includes("/examples")}
            href="/wiki/creating_a_game/examples">Examples</a
          >
        </li>
      {/snippet}
    </Dropdown>

    <hr />

    <li><a href="/" class:active={page.url.pathname === "/1"}>Test 2</a></li>
    <hr />

    <li><a href="/" class:active={page.url.pathname === "/2"}>Test 3</a></li>
  </ul>
</nav>

<style>
  .active {
    display: block; /* Forces the element to take up the full width available */
    width: 100%; /* Ensures it spans edge-to-edge */

    position: relative;
    border: none;
    border-top-right-radius: 1rem;
    border-bottom-right-radius: 1rem;
    isolation: isolate;

    /* If you use display: flex, you can align the text like this: */
    /* align-items: center; */
    /* padding-left: 1rem; */
  }

  /* Keyframes for sliding the mask from right to left */
  @keyframes border-wipe-left {
    0% {
      -webkit-mask-position:
        0% 0,
        0 0,
        0 0;
      mask-position:
        0% 0,
        0 0,
        0 0;
    }
    100% {
      -webkit-mask-position:
        100% 0,
        0 0,
        0 0;
      mask-position:
        100% 0,
        0 0,
        0 0;
    }
  }

  .active::after {
    content: "";
    position: absolute;
    inset: 0;
    border-radius: inherit;
    padding: 2px;
    background: linear-gradient(
      180deg,
      var(--nav-boarder-color-light),
      var(--nav-boarder-color-dark)
    );

    /* 
    Make the first layer (the fade) 200% wide so we have room to slide it.
    The other two layers remain standard size.
  */
    -webkit-mask:
      linear-gradient(to right, transparent, transparent 25%, #fff 75%, #fff)
        no-repeat,
      linear-gradient(#fff 0 0) content-box,
      linear-gradient(#fff 0 0);
    -webkit-mask-size:
      135% 100%,
      auto,
      auto;
    -webkit-mask-composite: source-in, xor;

    mask:
      linear-gradient(to right, transparent, transparent 25%, #fff 75%, #fff)
        no-repeat,
      linear-gradient(#fff 0 0) content-box,
      linear-gradient(#fff 0 0);
    mask-size:
      135% 100%,
      auto,
      auto;
    mask-composite: intersect, exclude;

    /* Apply the animation when the element renders */
    animation: border-wipe-left 0.8s ease-in-out both;
    pointer-events: none;
    z-index: -1;
  }

  nav {
    min-width: 8rem;
    width: 12rem;
    background-color: var(--nav-background-color);
    height: 90vh;
    overflow-y: auto;
  }

  /* List and dropdown layout */
  ul,
  :global(.dropdown-content) {
    list-style-type: none;
    display: flex;
    flex-direction: column;
  }

  li {
    margin: 0.5rem;
  }

  /* Navigation links */
  a,
  :global(.dropdown-toggle) {
    display: block;
    box-sizing: border-box;
    color: var(--text-color);

    padding: 1.3rem;
    padding-left: 3rem;

    text-align: right;
    text-decoration: none;
  }

  hr {
    width: 90%;
  }
</style>
