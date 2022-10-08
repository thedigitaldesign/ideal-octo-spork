<script lang="ts">
  /* 
    Time Tracking:
      Dinner: 05:30 to 06:10
  */
  // Svelte
  import { tick } from 'svelte'
  // Packages
  import { confetti } from '@neoconfetti/svelte'
  // Models
  import type { Downloads } from '../models'

  export let data: Downloads[]

  let selected: Downloads[] = []
  let checked: boolean
  let indeterminate: boolean
</script>

<template>
  <div>
    <table>
      <thead>
        <tr>
          <th><!-- Checkbox --></th>
          <th scope="col">Name</th>
          <th scope="col">Device</th>
          <th scope="col" class="min-w-[12rem]">Path</th>
          <th><!-- Indicator --></th>
          <th scope="col">Status</th>
        </tr>
      </thead>
      <tbody>
        {#each data as item}
          <tr class:bg-gray-50={selected.includes(item)}>
            <td class="relative w-12 px-6">
              <div class="selected-row-indicator w-[0.15rem] {selected.includes(item) ? 'bg-sky-300' : ''}" />
              
              <input 
                type="checkbox"
                class="checkbox"
                value={item}
                bind:group={selected}
              />
            </td>
            <td>{item.name}</td>
            <td>{item.device}</td>
            <td>{item.path}</td>
            <td>
              {#if item.status === 'available'}
                <div class="rounded-full bg-green-600 w-4 h-4 border-solid border-2 border-green-300 indicator-glow" />
              {/if}
            </td>
            <td>{item.status}</td>
          </tr>
        {/each}
      </tbody>
    </table>
  </div>
</template>

<style lang="less">
  table {
    @apply table-fixed divide-y divide-gray-400 min-w-full text-gray-900;

    thead {
      @apply bg-gray-50;

      th {
        @apply px-3 pt-4 pb-1 text-left text-xl font-normal;
      }
    }

    tbody {
      @apply divide-y divide-gray-200 bg-white;

      tr {
        @apply ease-in-out duration-200 hover:bg-gray-100;

        td {
          @apply whitespace-nowrap py-4 px-3 text-sm font-medium text-gray-800;
        }
      }
    }
  }

  .selected-row-indicator {
    @apply absolute inset-y-0 left-0 ease-in-out duration-300;
  }

  .availability-indicator {
    box-shadow: 0 0 4px rgb(74, 222, 128);
  }

  .checkbox {
    @apply -mt-2 h-4 w-4 rounded border-gray-300 text-sky-500 focus:ring-sky-400;
  }
</style>
