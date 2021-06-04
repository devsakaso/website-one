<template>
  <header class="header">
    <!-- 背景 -->
    <div class="header__logo-box">
        <img :src="require('@/assets/img/' + headerData.src)" alt="Logo" class="header__logo">
    </div>

    <div class="header__text-box">
        <!-- テキスト -->
        <h1 class="heading-primary">
            <span class="heading-primary--main">{{ headerData.title }}</span>
            <span class="heading-primary--sub">{{ headerData.subtitle }}</span>
        </h1>
        <!-- ボタン -->
        <a href="#book" class="btn btn--white btn--animated">{{ headerData.button }}</a>
    </div>
  </header>
</template>

<script>
export default {
  setup() {
    const headerData = {
        src: 'logo-white.svg',
        title: 'Outside of Japan',
        subtitle: 'is where life happen',
        button: '無料でパンフレットを取り寄せる'
    }

    return {
      headerData,
    }
  },
}
</script>

<style lang="scss" scoped>
.header {
    height: 85vh;
    background-image: linear-gradient(
        to right bottom,
        rgba($color-primary-light, 0.8),
        rgba($color-primary-dark, 0.8)),
    url(~@/assets/img/header.jpg);
    background-size: cover;
    background-position: center bottom;
    position: relative;
    

    @supports (clip-path: polygon(0 0)) or (-webkit-clip-path: polygon(0 0)) {
        -webkit-clip-path: polygon(0 0, 100% 0, 100% 75vh, 0 100%);
        clip-path: polygon(0 0, 100% 0, 100% 75vh, 0 100%);
        height: 95vh;
    }

    @media only screen and (min-resolution: 192dpi) and (min-width: 37.5em),
            only screen and (-webkit-min-device-pixel-ratio: 2) and (min-width: 37.5em),
            only screen and (min-width: 125em) {
        background-image: linear-gradient(
            to right bottom,
            rgba($color-primary-light, 0.8),
            rgba($color-primary-dark, 0.8)),
        url(~@/assets/img/header.jpg);
    }

    @include respond(phone) {
        -webkit-clip-path: polygon(0 0, 100% 0, 100% 85vh, 0 100%);
        clip-path: polygon(0 0, 100% 0, 100% 85vh, 0 100%);
    }

    &__logo-box {
        position: absolute;
        top: 4rem;
        left: 4rem;
    }

    &__logo {
        height: 3.5rem;
    }
    
    &__text-box {
        position: absolute;
        top: 40%;
        left: 50%;
        transform: translate(-50%, -50%);
        text-align: center;
    }
}
</style>