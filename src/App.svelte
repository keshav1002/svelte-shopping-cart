<script>
  import { v4 as uuidv4 } from "uuid";

  import Navbar from "./Navbar.svelte";
  import Card from "./Card.svelte";
  import Cart from "./Cart.svelte";

  let displayCart = false;
  let cartItems = [];
  let products = [
    {
      id: uuidv4(),
      title: "Book",
      description: "This is a book. Read the book.",
      price: 20.0,
      image: "./images/book.jpg",
    },
    {
      id: uuidv4(),
      title: "Car",
      description: "This is a car. Drive the car.",
      price: 200.0,
      image: "./images/car.jpg",
    },
    {
      id: uuidv4(),
      title: "House",
      description: "This is a house. Buy the house.",
      price: 2000.0,
      image: "./images/house.jpg",
    },
  ];

  function cartClicked(event) {
    displayCart = event.detail;
  }

  function homeClicked(event) {
    displayCart = event.detail;
  }

  function addToCart(event) {
    const selectedProdId = event.detail;
    const isAlreadyInCart = cartItems.findIndex(
      (prod) => prod.id === selectedProdId
    );
    if (isAlreadyInCart > -1) {
      cartItems[isAlreadyInCart].quantity += 1;
    } else {
      cartItems = [
        ...cartItems,
        { ...products.find((prod) => prod.id === selectedProdId), quantity: 1 },
      ];
    }
  }
</script>

<style>
  section {
    width: 80rem;
    margin: auto;
  }
</style>

<Navbar
  on:cartclicked={cartClicked}
  on:homeclicked={homeClicked}
  bind:cartItems />

{#if displayCart}
  <section>
    <Cart bind:cartItems />
  </section>
{:else}
  <section>
    {#each products as product}
      <Card
        on:addcart={addToCart}
        productId={product.id}
        productTitle={product.title}
        productPrice={product.price}
        productImage={product.image}>
        <p slot="description">{product.description}</p>
      </Card>
    {/each}
  </section>
{/if}
