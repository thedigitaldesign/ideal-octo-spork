<script lang="ts">
  /* 
    Time Tracking:
      Dinner: 05:30 to 06:10
      Stepped away: 06:50 to 07:05
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
  let explosion: boolean = false
  let disable: boolean

  const downloadSelected = async () => {
    explosion = false
    await tick()
    explosion = true

    let message: string = ''

    for (let i = 0; i < selected.length; i++) {
      message = message.concat('----------\n', 'Device: ' + selected[i].device + '\n', 'Path: ' + selected[i].path + '\n')
    }

    alert(`Download now! \n${message}`)
  }

  $: {
    indeterminate = selected.length > 0 && selected.length < data.length
    checked = checked && !indeterminate
    disable = selected.length > 0 && !selected.some((item) => item.status === 'scheduled')
  }
</script>

<template>
  <div>
    {#if explosion}
      <div>
        <div class="max-w-7xl m-auto" use:confetti />
      </div>
    {/if}
    <table>
      <thead>
        <tr>
          <th style="text-align: center;">
            <input type="checkbox" class="checkbox" bind:checked bind:indeterminate on:change={() => (selected = checked ? data.map((item) => item) : [])} />
          </th>
          <th>
            {#if selected.length}
              Selected {selected.length}
            {:else}
              None Selected
            {/if}
          </th>
          <th colspan="4">
            <button
              type="button"
              class="inline-flex items-center justify-center ease-in-out duration-200 enabled:hover:bg-gray-100 disabled:text-gray-400"
              disabled={!disable}
              on:click={downloadSelected}
            >
              <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 20 20" fill="currentColor" class="w-5 h-5 mr-2">
                <path
                  d="M10.75 2.75a.75.75 0 00-1.5 0v8.614L6.295 8.235a.75.75 0 10-1.09 1.03l4.25 4.5a.75.75 0 001.09 0l4.25-4.5a.75.75 0 00-1.09-1.03l-2.955 3.129V2.75z"
                />
                <path
                  d="M3.5 12.75a.75.75 0 00-1.5 0v2.5A2.75 2.75 0 004.75 18h10.5A2.75 2.75 0 0018 15.25v-2.5a.75.75 0 00-1.5 0v2.5c0 .69-.56 1.25-1.25 1.25H4.75c-.69 0-1.25-.56-1.25-1.25v-2.5z"
                />
              </svg>
              Download Selected
            </button>
          </th>
        </tr>
        <tr>
          <th><!-- Checkbox --></th>
          <th scope="col" class="min-w-[10rem]">Name</th>
          <th scope="col">Device</th>
          <th scope="col" class="min-w-[12rem]">Path</th>
          <th><!-- Indicator --></th>
          <th scope="col">Status</th>
        </tr>
      </thead>
      <tbody>
        {#each data as item}
          <tr class:bg-gray-50={selected.includes(item)}>
            <td class="relative w-12 px-6 text-center">
              <div class="selected-row-indicator w-[0.15rem] {selected.includes(item) ? 'bg-sky-300' : ''}" />

              <input type="checkbox" class="checkbox" value={item} bind:group={selected} />
            </td>
            <td>{item.name}</td>
            <td>{item.device}</td>
            <td>{item.path}</td>
            <td class="indicator-column">
              {#if item.status === 'available'}
                <div class="availability-indicator" />
              {/if}
            </td>
            <td class="capitalize">{item.status}</td>
          </tr>
        {/each}
      </tbody>
    </table>
  </div>
</template>

<style lang="less">
  table {
    @apply table-fixed divide-y divide-gray-300 min-w-full text-gray-900 shadow-lg;

    thead {
      @apply divide-y divide-gray-300;

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

          &.indicator-column {
            @apply pl-3 pr-0;
          }
        }
      }
    }
  }

  .selected-row-indicator {
    @apply absolute inset-y-0 left-0 ease-in-out duration-300;
  }

  .availability-indicator {
    @apply rounded-full bg-green-500 w-4 h-4 border-solid border-2 border-green-300 m-auto;
    box-shadow: 0 0 4px rgb(74, 222, 128);
  }

  .checkbox {
    @apply h-4 w-4 rounded border-gray-300 text-sky-500 focus:ring-sky-400;
  }
</style>
