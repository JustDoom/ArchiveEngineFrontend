<template>
  <div class="flex flex-col min-h-screen">
<!--    <Header/>-->
    <div class="basis-0 grow">
      <div class="ml-auto mr-auto my-8 w-[75%]">
        <nuxt/>
      </div>
    </div>
<!--    <Footer/>-->
  </div>
</template>

<style>
</style>

<script>
import Header from '../components/header'
import Footer from '../components/footer'

export default {
  components: {
    Footer,
    Header,
  },
}
</script>
