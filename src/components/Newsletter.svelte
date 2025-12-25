<script lang="ts">
  let email = $state('');
  let status = $state<'idle' | 'loading' | 'success' | 'error'>('idle');

  async function subscribe(e: Event) {
    e.preventDefault();
    status = 'loading';
    
    // Simulate API call
    await new Promise(resolve => setTimeout(resolve, 1000));
    
    status = 'success';
    email = '';
  }
</script>

<div class="border-t border-primary py-12 bg-off-white">
  <div class="max-w-md mx-auto px-4 text-center">
    <h3 class="font-serif text-2xl italic mb-4">Subscribe to the Editorial</h3>
    <p class="text-sm text-primary/60 mb-6 uppercase tracking-widest">Get the latest stories delivered to your inbox</p>
    
    <form onsubmit={subscribe} class="flex flex-col gap-4">
      <input 
        type="email" 
        bind:value={email} 
        placeholder="Your email address"
        required
        class="w-full px-4 py-3 bg-transparent border border-primary focus:outline-none focus:ring-1 focus:ring-primary placeholder:text-primary/40 font-serif"
        disabled={status === 'loading' || status === 'success'}
      />
      
      <button 
        type="submit"
        disabled={status === 'loading' || status === 'success'}
        class="w-full px-4 py-3 bg-primary text-off-white uppercase tracking-widest text-sm font-medium hover:bg-primary/90 transition-colors disabled:opacity-50 disabled:cursor-not-allowed"
      >
        {#if status === 'loading'}
          Subscribing...
        {:else if status === 'success'}
          Subscribed!
        {:else}
          Subscribe
        {/if}
      </button>
    </form>
  </div>
</div>
