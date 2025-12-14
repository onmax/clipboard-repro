<template>
  <div>
    <h1>Clipboard Repro</h1>
    <pre>{{ data }}</pre>
  </div>
</template>

<script setup>
// This runs on server during SSR, triggering the error overlay
const { data } = await useFetch('/api/error')
</script>
