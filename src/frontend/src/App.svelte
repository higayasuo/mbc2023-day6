<script>
  import Auth from "./components/Auth.svelte";
  import Calculator from "./components/Calculator.svelte";
</script>

<main>
  <a
    href="https://dfinity.org"
    target="_blank"
    rel="noopener noreferrer"
    class="logo"
  >
    <img src="images/dfinity.svg" alt="DFINITY logo" />
  </a>
  <h1>Calculator dApp</h1>
  <Auth />
  <Calculator />
</main>

<style>
  img {
    height: 22px;
  }
  .logo {
    display: inline-block;
    margin-bottom: 24px;
    margin-top: 24px;
  }

  main {
    text-align: center;
    padding: 1em;
  }

  h1 {
    font-size: 3em;
    font-weight: 400;
    line-height: 1.09;
    font-family: Georgia, "Times New Roman", Times, serif, sans-serif;
  }

  @media (min-width: 640px) {
    main {
      max-width: 800px;
      margin: 0 auto;
    }
    h1 {
      font-size: 4em;
    }
  }
</style>
