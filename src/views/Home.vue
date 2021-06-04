<template>
  <!-- ヘッダー -->
  <Header/>
  <!-- メイン -->
  <main>
    <section class="section-about" id="about">
     <About/>
    </section>

    <section class="section-features" id="features">
      <Features/>
    </section>

    <section class="section-tours" id="tours">
     <Tours/>
    </section>

    <section class="section-stories" id="stories">
     <Stories/>
    </section>

    <section class="section-book" id="book">
      <Book/>
    </section>
  </main>
</template>

<script>
import Header from '@/views/home/Header.vue'
import About from '@/views/home/About.vue'
import Features from '@/views/home/Features.vue'
import Tours from '@/views/home/Tours.vue'
import Stories from '@/views/home/Stories.vue'
import Book from '@/views/home/Book.vue'

export default {
    name: 'Home',
    components: {
    Header,
    About,
    Features,
    Tours,
    Stories,
    Book,
  },

}
</script>