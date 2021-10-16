<script>
  import { identity } from 'svelte/internal';
import logo from './assets/svelte.png'
  import Counter from './lib/Counter.svelte'

  let name = 'you';

  let user = { loggedIn: false};

  function toggle() {
    user.loggedIn = !user.loggedIn;
  }

  let videos = [
    { id: 'kpMwxnsbg0Y', name: 'Snowmen' },
    { id: 'De4jPjoHatA', name: 'Doggo' }
  ];

  async function getRandomNumber() {
      const res = await fetch(`tutorial/random-number`);
      const text = await res.text();

      if (res.ok) {
        return text;
      } 
      else {
        throw new Error(text);
      }
    }
    let promise = getRandomNumber();

    function handleClick() {
      promise = getRandomNumber();
    }
</script>

<main>
  <img src={logo} alt="Svelte Logo" />
  <h1>Hello world!</h1>
  <h2>Hello {name}!</h2>

  <Counter />

  {#if user.loggedIn}
    <button on:click={toggle}>
      Log out
    </button>
  {:else}
    <button on:click={toggle}>
      Log in
    </button>
  {/if}

  <p>
    Visit <a href="https://svelte.dev">svelte.dev</a> to learn how to build Svelte
    apps.
  </p>

  <p>
    Check out <a href="https://github.com/sveltejs/kit#readme">SvelteKit</a> for
    the officially supported framework, also powered by Vite!
  </p>

  <h3>Just two cause I could only find these two &#128517;</h3>

  <ul>
    {#each videos as {id, name}}
      <li><a target="_blank" href="https://www.youtube.com/watch?v={id}">
        {name}
      </a></li>
    {/each}
  </ul>

  <button on:click={handleClick}>
    generate random number
  </button>

  
  {#await promise}
	  <p>...waiting</p>
  {:then number}
	  <p>The number is {number}</p>
  {:catch error}
	    <p style="color: red">{error.message}</p>
  {/await}
  
  
</main>


<style>
  :root {
    font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen,
      Ubuntu, Cantarell, 'Open Sans', 'Helvetica Neue', sans-serif;
  }

  main {
    text-align: center;
    padding: 1em;
    margin: 0 auto;
  }

  img {
    height: 16rem;
    width: 16rem;
  }

  h1 {
    color: #ff3e00;
    text-transform: uppercase;
    font-size: 4rem;
    font-weight: 100;
    line-height: 1.1;
    margin: 2rem auto;
    max-width: 14rem;
  }

  h2 {
    color: pink;
    font-family: 'Georgia';
    font-size: 3em;
  }

  ul {
    text-align: center;
    list-style-position: inside;
  }

  p {
    max-width: 14rem;
    margin: 1rem auto;
    line-height: 1.35;
  }

  @media (min-width: 480px) {
    h1 {
      max-width: none;
    }

    p {
      max-width: none;
    }
  }
</style>
