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

    <li>
      <a
        href="/wiki/setup-and-installation"
        class:active={page.url.pathname.includes("/setup-and-installation")}
        >Setup and Installation</a
      >
    </li>
    <hr />

    <Dropdown title="Basics" open={page.url.pathname.includes("/basics")}>
      {#snippet children()}
        <li>
          <a
            class:active={page.url.pathname.includes("/creating-your-game")}
            href="/wiki/basics/creating-your-game">Creating your game</a
          >
        </li>
        <li>
          <a
            class:active={page.url.pathname.includes(
              "/settings-and-configuration",
            )}
            href="/wiki/basics/settings-and-configuration"
            >Settings and Configuration</a
          >
        </li>
        <li>
          <a
            class:active={page.url.pathname.includes("/using-the-UI")}
            href="/wiki/basics/using-the-UI">Using the UI</a
          >
        </li>
        <li>
          <a
            class:active={page.url.pathname.includes("/drawing")}
            href="/wiki/basics/drawing">Drawing</a
          >
        </li>
        <li>
          <a
            class:active={page.url.pathname.includes("/updating")}
            href="/wiki/basics/updating">Updating</a
          >
        </li>
        <li>
          <a
            class:active={page.url.pathname.includes("/cursors")}
            href="/wiki/basics/cursors">Cursors</a
          >
        </li>
      {/snippet}
    </Dropdown>
    <hr />

    <Dropdown title="Advanced" open={page.url.pathname.includes("/advanced")}>
      {#snippet children()}
        <li>
          <a
            class:active={page.url.pathname.includes("/advanced-UI")}
            href="/wiki/advanced/advanced-UI">Advanced UI</a
          >
        </li>
        <li>
          <a
            class:active={page.url.pathname.includes("/transforms")}
            href="/wiki/advanced/transforms">Transforms</a
          >
        </li>
      {/snippet}</Dropdown
    >
    <hr />

    <Dropdown title="Java" open={page.url.pathname.includes("/java")}>
      {#snippet children()}
        <li>
          <a
            class:active={page.url.pathname.includes("/interfaces")}
            href="/wiki/java/interfaces">Interfaces</a
          >
        </li>
        <li>
          <a
            class:active={page.url.pathname.includes("/records")}
            href="/wiki/java/records">Records</a
          >
        </li>
        <li>
          <a
            class:active={page.url.pathname.includes("/instanceof")}
            href="/wiki/java/instanceof">instanceof</a
          >
        </li>
        <li>
          <a
            class:active={page.url.pathname.includes("/loops")}
            href="/wiki/java/loops">Advanced loops</a
          >
        </li>
        <li>
          <a
            class:active={page.url.pathname.includes("/threads")}
            href="/wiki/java/threads">Threads</a
          >
        </li>
      {/snippet}
    </Dropdown>
    <hr />
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
    animation: border-wipe-left 0.5s ease-in-out both;
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

  ul,
  :global(.dropdown-content) {
    list-style-type: none;
  }

  li {
    margin: 0.5rem;
  }

  /* Navigation links */
  a {
    display: block;
    box-sizing: border-box;
    color: var(--text-color);
    padding: 1.3rem;
    text-align: right;
    text-decoration: none;
  }

  :global(.dropdown-toggle) {
    display: block;
    box-sizing: border-box;
    color: var(--text-color);

    background-color: transparent;
    border: none;

    border-top-right-radius: 1rem;
    border-bottom-right-radius: 1rem;

    position: relative;

    width: 87.5%;
    margin: 0.5rem 0.5rem 0.5rem 1rem;

    padding: 1.3rem;

    text-align: right;
  }

  hr {
    width: 90%;
  }
</style>
