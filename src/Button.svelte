<style>
  button {
    font: inherit;
    padding: 0.5rem;
    background: #ff9900;
    border: 1px solid #ff9900;
    border-radius: 0.5rem;
    color: white;
    cursor: pointer;
  }

  button:hover,
  button:active {
    box-shadow: 1px 1px 6px rgba(0, 0, 0, 0.26);
  }
</style>

<button on:click>
  <slot />
</button>
