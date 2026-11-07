<script></script>

<body>
  <header>
    <nav>
      <ul>
        <li class="left-align"><a href="/">SwingSet</a></li>
        <li><a href="/wiki">Wiki</a></li>
        <li><a href="/use">Use</a></li>
        <li>
          <a href="https://galactica.nrds.xyz/SwingSet%20Engine%20API/"
            >Javadoc</a
          >
        </li>
        <li>
          <a href="https://github.com/GA1ACTICA/SwingSet_Engine">Github</a>
        </li>
      </ul>
    </nav>
  </header>
</body>

<style>
  header {
    height: 10vh;
    background-color: gray;
  }

  nav {
    height: 9.8vh;
    width: 100vw;
    background-color: var(--nav-background-color);
  }

  ul {
    list-style-type: none;
    justify-content: right;
    display: flex;

    margin-right: 3rem;
  }

  li {
    padding: 0.5rem;
    margin: 1.5rem;
    margin-top: 0.4rem;

    border-bottom-left-radius: 1rem;
    border-bottom-right-radius: 1rem;

    mask-image: linear-gradient(180deg, transparent 0%, black 30%);
    -webkit-mask-image: linear-gradient(180deg, transparent 0%, black 30%);
  }

  a {
    color: var(--text-color);

    text-decoration: none;
  }

  .left-align {
    margin-right: auto;
  }
</style>
