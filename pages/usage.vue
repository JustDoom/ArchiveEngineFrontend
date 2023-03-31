<template>
  <div class="main-body">
    <h1 class="text-center font-bold text-5xl">Archive Engine</h1><br>
    <div>
      <NuxtLink to="/">Back to Search</NuxtLink> -
      <NuxtLink to="/statistics">Statistics</NuxtLink><br><br>
      <p>This is an early version of this website so there will be issues. This is not at all the final version of the website and will work on fixing any issues over time. I just wanted to get a minimal version out for testing quickly.</p><br>
      <h2 class="font-bold text-2xl">Usage</h2>
      <p>There are some rules to get it to work properly until it is fixed so read this. Searching only matches your word in a link exactly (ignoring cases). So searching for "bukit" would only find any links containing that exact text. It also only words with one word for now (will be updated soon). The timestamps are when the link was archived and not when they were created.</p><br>
      <h2 class="font-bold text-2xl">Open Source</h2>
      <p>This is also open source!</p>
      <a href="https://github.com/JustDoom/ArchiveEngineBackend" target="_blank">Backend Repository</a><br>
      <a href="https://github.com/JustDoom/ArchiveEngineFrontend" target="_blank">Frontend Repository</a>
    </div>
  </div>
</template>

<script>
export default {
  name: "index"
}
</script>

<style>
</style>