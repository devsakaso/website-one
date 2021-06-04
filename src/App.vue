<template>
<Navigation/>
<Home/>
<Footer/>
</template>

<script>
import Navigation from '@/components/Navigation.vue'
import Home from '@/views/Home.vue'
import Footer from '@/views/Footer.vue'

export default {
  name: 'App',
  components: {
    Navigation,
    Home,
    Footer,
  }
}
</script>