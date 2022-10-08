<script lang="ts">
  // Components
  import SelectTable from '../components/SelectTable.svelte'
  // Models
  import type { Downloads } from '../models'

  const blob: Downloads[] = [
    { name: 'smss.exe', device: 'Stark', path: '\\Device\\HarddiskVolume2\\Windows\\System32\\smss.exe', status: 'scheduled' },
    { name: 'netsh.exe', device: 'Targaryen', path: '\\Device\\HarddiskVolume2\\Windows\\System32\\netsh.exe', status: 'available' },
    { name: 'uxtheme.dll', device: 'Lanniester', path: '\\Device\\HarddiskVolume1\\Windows\\System32\\uxtheme.dll', status: 'available' },
    { name: 'cryptbase.dll', device: 'Martell', path: '\\Device\\HarddiskVolume1\\Windows\\System32\\cryptbase.dll', status: 'scheduled' },
    { name: '7za.exe', device: 'Baratheon', path: '\\Device\\HarddiskVolume1\\temp\\7za.exe', status: 'scheduled' }
  ]
</script>

<svelte:head>
  <title>Joshua (Josh) Christensen - Coding Assessment</title>
  <meta name="description" content="Through the fire and flames we carry on!" />
</svelte:head>

<template>
  <div class="content">
    <SelectTable data={blob} />
  </div>
</template>

<style lang="less">
  .content {
    @apply max-w-7xl m-auto py-10;
  }
</style>
