<script>
  import arrow from "$lib/assets/arrow-up.svg";
  let { title, children, open = $bindable(false) } = $props();
</script>

<div class="dropdown">
  <button class="dropdown-toggle" onclick={() => (open = !open)}>
    {title}
    <img src={arrow} alt="Toggle arrow" class="arrow-icon" class:open />
  </button>

  {#if open}
    <ul class="dropdown-content">
      {@render children()}
    </ul>
  {/if}
</div>

<style>
  .dropdown-toggle {
    background-color: transparent;
    margin: 0.5rem;
    border-top-right-radius: 1rem;
    border-bottom-right-radius: 1rem;
    border: none;
    position: relative;
  }

  .dropdown-toggle::after {
    content: "";
    position: absolute;
    inset: 0;
    border-radius: inherit;
    padding: 2px;
    background: linear-gradient(
      180deg,
      var(--dropdown-boarder-color-light, #999),
      var(--dropdown-boarder-color-dark, #333)
    );

    /* 
      Layer 1: The horizontal fade
      Layer 2: The inner cutout (content-box)
      Layer 3: The full outer shape
    */
    -webkit-mask:
      linear-gradient(to right, transparent 0%, black 40%),
      linear-gradient(black 0 0) content-box,
      linear-gradient(black 0 0);

    -webkit-mask-composite: source-in, xor;

    mask:
      linear-gradient(to right, transparent 0%, black 40%),
      linear-gradient(black 0 0) content-box,
      linear-gradient(black 0 0);

    mask-composite: intersect, exclude;

    pointer-events: none;
  }

  .arrow-icon {
    width: 1rem;
    height: 1rem;
    display: inline-block;
    vertical-align: middle;
    transition: transform 0.3s ease;
    filter: brightness(0) invert(1);
  }

  .arrow-icon.open {
    transform: rotate(180deg);
  }
</style>
