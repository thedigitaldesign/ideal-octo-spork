<script lang="ts">
  /* 
    Time Tracking:
      Dinner: 05:30 to 06:10
  */
  // Svelte
  import {tick} from 'svelte'
  // Packages
  import { confetti } from '@neoconfetti/svelte'
  // Models
  import type { Downloads } from '../models'

  export let data: Downloads[]

  let selected: Downloads[]
  
</script>

<template>
  <div>
    

    <table >
      <thead>
        <tr>
          <th><!-- Checkbox --></th>
          <th>Name</th>
          <th>Device</th>
          <th>Path</th>
          <th><!-- Indicator --></th>
          <th>Status</th>
        </tr>
      </thead>
      <tbody>
        {#each data as item}
           <tr>
            <td>Checkbox</td>
            <td>{item.name}</td>
            <td>{item.device}</td>
            <td>{item.path}</td>
            <td>Indicator</td>
            <td>{item.status}</td>
           </tr>
        {/each}
      </tbody>
    </table>
  </div>
</template>

<style lang="less">
  table {
    @apply table-fixed divide-y divide-gray-400 min-w-full;

    th {
      @apply px-3 py-4;
      // padding-top: 0.875rem;
      // padding-bottom: 0.875rem;
    }
  }
</style>
