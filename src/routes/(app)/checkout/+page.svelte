<script>
  import { Input } from '$lib/components/ui/input';
  import { Textarea } from '$lib/components/ui/textarea';
  import { Button } from '$lib/components/ui/button';
  import {
    Dialog,
    DialogTrigger,
    DialogContent,
    DialogHeader,
    DialogTitle,
    DialogDescription
  } from '$lib/components/ui/dialog';

  let customerName = '';
  let contactNumber = '';
  let address = '';
  let paymentMethod = 'Credit Card';
  let showDialog = false;

  let orderedItems = [
    { name: 'Product A', quantity: 2, price: 100 },
    { name: 'Product B', quantity: 1, price: 50 }
  ];

  $: finalTotal = orderedItems.reduce((sum, item) => sum + item.price * item.quantity, 0);
</script>

<!-- Light brown background wrapper -->
<div class="min-h-screen bg-[#f5e6d3] py-10">
  <div class="max-w-3xl mx-auto p-6 bg-white rounded-lg shadow-md">
    <h1 class="text-3xl font-bold mb-6 text-[#800000]">🧾 Checkout</h1>

    <form class="space-y-5">
      <div>
        <label class="block mb-1 font-semibold text-gray-700">Customer Name</label>
        <Input bind:value={customerName} placeholder="Enter your name" />
      </div>

      <div>
        <label class="block mb-1 font-semibold text-gray-700">Contact Number</label>
        <Input type="tel" bind:value={contactNumber} placeholder="e.g. 09123456789" />
      </div>

      <div>
        <label class="block mb-1 font-semibold text-gray-700">Address</label>
        <Textarea bind:value={address} placeholder="Enter your address" />
      </div>

      <div>
        <label class="block mb-1 font-semibold text-gray-700">Payment Method</label>
        <select
          bind:value={paymentMethod}
          class="w-full border rounded px-3 py-2 bg-white text-gray-800 focus:outline-none focus:ring-2 focus:ring-[#800000]"
        >
          <option value="Credit Card">Credit Card</option>
          <option value="PayPal">PayPal</option>
          <option value="Cash on Delivery">Cash on Delivery</option>
        </select>
      </div>
    </form>

    <div class="mt-8">
      <h2 class="text-xl font-semibold mb-2 text-gray-800">🧮 Order Summary</h2>
      <ul class="mb-4 text-gray-700">
        {#each orderedItems as item}
          <li>{item.quantity} x {item.name} - ${item.price * item.quantity}</li>
        {/each}
      </ul>
      <p class="font-bold text-lg">Final Total: ${finalTotal}</p>
    </div>

    <Dialog open={showDialog} on:openChange={(v) => showDialog = v}>
      <DialogTrigger>
        <Button class="mt-6 bg-[#800000] text-white hover:bg-[#990000]" on:click={() => showDialog = true}>
          Submit Order
        </Button>
      </DialogTrigger>
      <DialogContent class="bg-[#800000] text-white rounded-lg">
        <DialogHeader>
          <DialogTitle>✅ Order Submitted</DialogTitle>
          <DialogDescription>Your order has been successfully placed!</DialogDescription>
        </DialogHeader>
      </DialogContent>
    </Dialog>
  </div>
</div>
