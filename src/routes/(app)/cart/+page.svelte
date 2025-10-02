<script>
  import { Button } from '$lib/components/ui/button';
  import IconTrash from 'lucide-svelte/icons/trash';

  let cartItems = [
    { id: 1, name: 'Spanish Latte', price: 100, quantity: 2 },
    { id: 2, name: 'Hot Americano', price: 50, quantity: 1 }
  ];

  function removeItem(id) {
    cartItems = cartItems.filter(item => item.id !== id);
  }

  function updateQuantity(id, qty) {
    cartItems = cartItems.map(item =>
      item.id === id ? { ...item, quantity: qty } : item
    );
  }

  $: totalItems = cartItems.reduce((sum, item) => sum + item.quantity, 0);
  $: totalPrice = cartItems.reduce((sum, item) => sum + item.price * item.quantity, 0);
</script>

<!-- Light brown background wrapper -->
<div class="min-h-screen bg-[#f5e6d3] py-10">
  <div class="max-w-4xl mx-auto p-6 bg-white rounded-lg shadow-md">
    <h1 class="text-3xl font-bold mb-6 text-[#800000]">🛒 Your Cart</h1>

    <table class="w-full border rounded overflow-hidden mb-6">
      <thead class="bg-gray-100 text-gray-700">
        <tr>
          <th class="p-3 text-left">Product Name</th>
          <th class="p-3 text-left">Price</th>
          <th class="p-3 text-left">Quantity</th>
          <th class="p-3 text-left">Subtotal</th>
          <th class="p-3 text-left">Remove</th>
        </tr>
      </thead>
      <tbody>
        {#each cartItems as item}
          <tr class="border-t">
            <td class="p-3">{item.name}</td>
            <td class="p-3">${item.price}</td>
            <td class="p-3">
              <input
                type="number"
                min="1"
                value={item.quantity}
                on:input={(e) => updateQuantity(item.id, +e.target.value)}
                class="w-16 border rounded px-2 py-1"
              />
            </td>
            <td class="p-3 font-medium">${item.price * item.quantity}</td>
            <td class="p-3">
              <button
                class="p-2 rounded hover:bg-red-100"
                on:click={() => removeItem(item.id)}
              >
                <IconTrash class="w-5 h-5 text-red-600" />
              </button>
            </td>
          </tr>
        {/each}
      </tbody>
    </table>

    <div class="flex justify-between items-center border-t pt-4">
      <div class="text-gray-700">
        <p>Total Items: <strong>{totalItems}</strong></p>
        <p>Total Price: <strong>${totalPrice}</strong></p>
      </div>
      <Button as="a" href="/checkout" class="bg-[#800000] text-white hover:bg-[#990000]">
        Proceed to Checkout
      </Button>
    </div>
  </div>
</div>
