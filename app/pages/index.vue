<script setup>

</script>

<template>
  <!-- These are Nuxt components and will get hoisted into how the page is built -->
  <Html>
    <!-- Html not necessarily needed, but is available if need to customize -->
    <Head>
      <Title>You're Home</Title>
      <!-- This allows you to completely split up resources throughout the app,
            at a component level -->
      <Link
        rel="stylesheet"
        href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.2.0/css/all.min.css"
      />
      <Link rel="preconnect" href="https://fonts.googleapis.com" />
      <Link rel="preconnect" href="https://fonts.gstatic.com" crossorigin />
      <Link href="https://fonts.googleapis.com/css2?family=Poor+Story&display=swap" rel="stylesheet" />
    </Head>
  </Html>
  <NuxtLayout>
    <h1 class="title">Home Page</h1>
    <h2 class="subtitle">This is a <i class="fa-brands fa-vuejs"></i>ue project</h2>
  </NuxtLayout>
</template>

<style lang="scss">
body {
  font-family: 'Poor Story', cursive !important;
}
</style>