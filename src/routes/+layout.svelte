<script lang="ts">
  // Svelte
  import { tick } from 'svelte'
  // Styles
  import '../assets/css/tailwind.css'
  // Packages
  import { confetti } from '@neoconfetti/svelte'

  let powww: boolean = false

  const explosion = async () => {
    powww = false
    await tick()
    powww = true
  }
</script>

<template>
  <div class="app">
    {#if powww}
      <div>
        <div class="max-w-7xl m-auto" use:confetti={{duration: 50000, particleShape: 'circles'}} />
      </div>
    {/if}
    
    <main>
      <slot>Oops! Something wen't wrong</slot>
    </main>
  </div>

  <footer>
    <p on:click={explosion}>This is one cool footer!</p>
  </footer>
</template>

<style lang="less">
  footer {
    @apply flex flex-col justify-center items-center py-3;
  }
</style>
