<script>
  import { createEventDispatcher } from "svelte";

  export let cartItems;
  $: cartLength = cartItems.length;

  let activeLink = "home";
  const dispatch = createEventDispatcher();

  function cartClicked() {
    dispatch("cartclicked", true);
    activeLink = "cart";
  }

  function homeClicked() {
    dispatch("homeclicked", false);
    activeLink = "home";
  }
</script>

<style>
  ul.topnav {
    list-style-type: none;
    margin: 0;
    padding: 0;
    overflow: hidden;
    background-color: #232f3e;
  }

  ul.topnav li {
    float: left;
  }

  ul.topnav li a {
    display: block;
    color: white;
    text-align: center;
    padding: 1.5rem 1rem;
    text-decoration: none;
  }

  ul.topnav li a:hover:not(.active) {
    background-color: #111;
  }

  ul.topnav li a.active {
    background-color: #ff9900;
  }

  ul.topnav li.right {
    float: right;
  }

  .logo {
    padding: 0.6rem 1rem 0rem 1rem;
    height: 3rem;
    width: 3rem;
  }

  .cart {
    padding: 0rem 1rem 0rem 0.2rem;
    height: 0.9rem;
    width: 0.9rem;
  }

  .badge {
    width: 1.5rem;
    background-color: #ff9900;
    border-radius: 20rem;
    float: right;
  }

  @media screen and (max-width: 600px) {
    ul.topnav li.right,
    ul.topnav li {
      float: none;
    }
  }
</style>

<ul class="topnav">
  <li>
    <img class="logo" src="./images/logo.png" alt="Logo" />
  </li>
  <li>
    <a
      class:active={activeLink === 'home'}
      href
      on:click|preventDefault={homeClicked}>
      Home
    </a>
  </li>
  <li class="right">
    <a
      class:active={activeLink === 'cart'}
      href
      on:click|preventDefault={cartClicked}>
      Cart
      <img class="cart" src="./images/cart.png" alt="Cart" />
      {#if cartLength > 0}
        <div class="badge">{cartLength}</div>
      {/if}
    </a>
  </li>
</ul>
