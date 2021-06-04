<template>
  <div class="popup" id="popup">
    <div class="popup__content">
      <div class="popup__left">
        <img v-for="item in popupData.images" :key="item.src" :src="require('@/assets/img/'+ item.src)" :alt="item.alt" class="popup__img">
      </div>
      <div class="popup__right">
        <button class="popup__close" @click="close">&times;</button>
        <h2 class="heading-secondary u-margin-bottom-small">{{ popupData.title }}</h2>
        <h3 class="heading-tertiary u-margin-bottom-small">{{ popupData.subtitle }}</h3>
        <p class="popup__text">
            {{ popupData.text }}
        </p>
        <a href="#" class="btn btn--green">{{ popupData.button }}</a>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  setup(props, context) {
    const popupData = {
      images: [
        {
          src: 'about-1.jpg',
          alt: 'Photo One'
        },
        {
          src: 'about-3.jpg',
          alt: 'Photo Two'
        },
      ],
      title: 'ご利用前にご確認ください',
      subtitle: 'Lorem ipsum dolor sit amet',
      text: 'Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.Sed sed risus pretium quam. Aliquam sem et tortor consequat id. Volutpat odio facilisis mauris sitamet massa vitae. Mi bibendum neque egestas congue. Placerat orci nulla pellentesque dignissim enimsit. Vitae semper quis lectus nulla at volutpat diam ut venenatis. Malesuada pellentesque elit egetgravida cum sociis natoque penatibus et. Proin fermentum leo vel orci porta non pulvinar neque laoreet.Gravida neque convallis a cras semper. Molestie at elementum eu facilisis sed odio morbi quis. Faucibusvitae aliquet nec ullamcorper sit amet risus nullam eget. Nam libero justo laoreet sit. Amet massavitae tortor condimentum lacinia quis vel eros donec. Sit amet facilisis magna etiam. Imperdiet sedeuismod nisi porta.',
      button: '無料で資料を請求する'
    }
    const close = () => {
      context.emit('close')
    }

    return {
      popupData,
      close,
    }
  },
}
</script>

<style lang="scss" scoped>
.popup {
    height: 100vh;
    width: 100%;
    position: fixed;
    top: 0;
    left: 0;
    background-color: rgba($color-black, .8);
    z-index: 9999;
    transition: all .3s;

    @supports (-webkit-backdrop-filter: blur(10px)) or (backdrop-filter: blur(10px)) {
        -webkit-backdrop-filter: blur(10px);
        backdrop-filter: blur(10px);
        background-color: rgba($color-black, .3);
    }

    &__content {
        @include absCenter;

        width: 75%;
        background-color: $color-white;
        box-shadow: 0 2rem 4rem rgba($color-black, .2);
        border-radius: 3px;
        display: table;
        overflow: hidden;
        opacity: 0;
        transition: all .3s .2s;

        @include respond(tab-port) {
            width: 90%;
            overflow: auto;
        }

        @include respond(phone) {
            position: relative;
            display: block;
        }
    }

    &__left {
        width: 33.333333%;
        display: table-cell;

        @include respond(phone) {
            width: 100%;
            display: block;
        }
    }

    &__right {
        width: 66.6666667%;
        display: table-cell;
        vertical-align: middle;
        padding: 3rem 5rem;

        @include respond(phone) {
            width: 100%;
            display: block;
        }
    }

    &__img {
        display: block;
        width: 100%;

        @include respond(phone) {
            display: hidden;
            width: 0%;
        }
    }

    &__text {
        font-size: 1.4rem;
        margin-bottom: 4rem;

        column-count: 2;
        column-gap: 4rem;
        column-rule: 1px solid $color-grey-light-2;

        hyphens: auto;

        @include respond(phone) {
            column-count: 1;
        }
    }

    //表示中
    &.is-active {
        opacity: 1;
        visibility: visible;
    }

    &.is-active &__content {
        opacity: 1;
    }

    // 閉じるボタン
    &__close {
            color: $color-grey-dark;
            position: absolute;
            top: 2.5rem;
            right: 2.5rem;
            font-size: 3rem;
            text-decoration: none;
            display: inline-block;
            transition: all .2s;
            line-height: 1;
            background: transparent;
            border: none;
            cursor: pointer;

        &:hover {
            color: $color-primary;
        }
    }
}
</style>