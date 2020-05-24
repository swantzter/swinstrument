<template>
  <main>
    <h1>Swinstrument</h1>
    <h2>This is NOT Swish</h2>
    <p>
      This is just to help you practice playing swish the musical instrument
      without ruining yourself.
    </p>
    <p>
      The source code is available on GitHub:
      <a href="https://github.com/svbeon/swinstrument" target="_blank" rel="noopener">svbeon/swinstrument</a>.
      You probably don't want to look at the source though - I haven't used the appropriate tools for the task,
      I just wanted to try <a href="https://github.com/vitejs/vite" target="_blank" rel="noopener">vitejs/vite</a>
    </p>
    <br />
    <img src="/img/source.png" alt="Logo" />
  </main>
  <footer>
    &copy; <a href="https://swantzter.se" target="_blank" rel="noopener">Swantzter</a> 2020, Logo &copy; Niniponken 2020
  </footer>
</template>

<style scoped>
main, footer {
  padding-right: 1rem;
  padding-left: 1rem;
}

main {
  max-height: 50vh;
  overflow-y: auto;
  text-align: center;
  padding-top: 2rem;
  padding-bottom: 2rem;
  font-size: .8rem;
}

footer {
  position: fixed;
  bottom: 0;
  padding-bottom: .2rem;
  color: #444;
  font-size: .7rem;
}

h2 {
  color: #ff4136;
  font-size: 1.3rem;
}

a {
  text-decoration: none;
  color: #0074d9;
  transition: .3s color;
}

a:hover {
  color: #7fdbff;
}

@media (prefers-color-scheme: dark) {
  footer {
    color: #ccc;
  }

  a {
    color: #7fdbff;
  }

  a:hover {
    color: #0074d9;
  }
}

img {
  width: 15vw;
}
</style>
