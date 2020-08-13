<script>
  export let cartItems;

  $: cartTotal = cartItems.reduce((sum, curValue) => {
    return sum + curValue.price * curValue.quantity;
  }, 0);

  function getSubtotal(item) {
    return item.price * item.quantity;
  }

  function removeItem(id) {
    cartItems = cartItems.filter(function (item) {
      return item.id !== id;
    });
  }
</script>

<style>
  .cart {
    border-radius: 1rem;
    border-collapse: collapse;
    width: 100%;
    margin: 5.5rem 1.5rem 1.5rem 1.5rem;
  }

  .cart td,
  .cart th {
    border: 1px solid #ddd;
    padding: 8px;
  }

  .cart tr:nth-child(even) {
    background-color: #f2f2f2;
  }

  .cart tr:hover {
    background-color: #ddd;
  }

  .cart th {
    padding-top: 12px;
    padding-bottom: 12px;
    text-align: left;
    background-color: #146eb4;
    color: white;
  }

  .total-label {
    float: right;
  }

  .trash {
    width: 1rem;
    cursor: pointer;
  }
</style>

{#if cartItems.length === 0}
  <p>No items in cart yet.</p>
{:else}
  <table class="cart">
    <tr>
      <th>Title</th>
      <th>Price</th>
      <th>Quantity</th>
      <th>Subtotal</th>
      <th />
    </tr>
    {#each cartItems as item}
      <tr>
        <td>{item.title}</td>
        <td>${item.price}.00</td>
        <td>
          <input type="number" id="price" bind:value={item.quantity} />
        </td>
        <td>{getSubtotal(item)}</td>
        <td on:click={removeItem(item.id)}>
          <img class="trash" src="./images/trash.png" alt="trash" />
        </td>
      </tr>
    {/each}
  </table>
{/if}

<h1 class="total-label">TOTAL: ${cartTotal}</h1>
