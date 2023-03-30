<template>
  <div class="flex flex-col min-h-screen">
<!--    <Header/>-->
    <div class="basis-0 grow">
      <div class="ml-[50%] my-8 transform -translate-x-1/2 w-[70%]">
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
