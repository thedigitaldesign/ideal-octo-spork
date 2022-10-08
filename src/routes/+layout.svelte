<script lang="ts">
  import '../assets/css/tailwind.css'
</script>

<template>
  <div class="app">
    <main>
      <slot>Oops! Something wen't wrong</slot>
    </main>
  </div>

  <footer>
    <p>
      This is some cool footer!
    </p>
  </footer>
</template>

<style lang="less">
  footer {
    @apply flex flex-col justify-center items-center py-3;
  }
</style>