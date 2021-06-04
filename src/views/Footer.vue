<template>
  <footer class="footer">
    <!-- ロゴ -->
      <div class="footer__logo-box">
          <img class="footer__logo" alt="logo" :src="require('@/assets/img/'+footerData.logoImage)">
      </div>

      <div class="row">
          <!-- フッターナブ -->
          <div class="col-1-of-2">
              <div class="footer__navigation">
                  <ul class="footer__list">
                      <li class="footer__item" v-for="(item, index) in footerData.navLists" :key="index">
                        <a :href="item.link" class="footer__link">{{ item.text }}</a>
                        </li>
                  </ul>
              </div>
          </div>
          <!-- コピーライト -->
          <div class="col-1-of-2">
              <p class="footer__copyright">
                  &copy; {{ footerData.copyDetails.year }} <a :href="footerData.copyDetails.link" class="footer__link">{{ footerData.copyDetails.name }}</a>. All right reserved
              </p>
          </div>
      </div>
  </footer>
</template>

<script>
export default {
  setup() {
    const footerData = {
      logoImage: 'icon.png',
      navLists: [
        {
          link: '#',
          text: '運営会社'
        },
        {
          link: '#',
          text: 'お問い合わせ'
        },
        {
          link: '#',
          text: '採用情報'
        },
        {
          link: '#',
          text: 'プライバシーポリシー'
        },
        {
          link: '#',
          text: 'ヘルプ'
        },
      ],
      copyDetails:{
        year: 2021,
        link: 'https://www.sakaso-portfolio.com/',
        name: 'Sakai'
      }

    }

    return {
      footerData,
    }
  },
}
</script>

<style lang="scss" scoped>
.footer {
    background-color: $color-grey-dark-3;
    padding: 10rem 0;
    font-size: 1.4rem;
    color: $color-grey-light-1;

    @include respond(tab-port) {
        padding: 8rem 0;
    }

    &__logo-box {
        text-align: center;
        margin-bottom: 8rem;

        @include respond(tab-port) {
            margin-bottom: 6rem;
        }
    }

    &__logo {
        width: 10rem;
        height: 10rem;
    }

    &__navigation {
        border-top: 1px solid $color-grey-dark;
        padding-top: 2rem;
        display: inline-block;

        @include respond(tab-port) {
            width: 100%;
            text-align: center;
        }
    }

    &__list {
        list-style: none;
    }

    &__item {
        display: inline-block;

        &:not(:last-child) {
            margin-right: 1.5rem;
        }
    }

    &__link {
        &:link,
        &:visited {
            color: $color-grey-light-1;
            background-color: $color-grey-dark-3;
            text-decoration: none;
            text-transform: uppercase;
            display: inline-block;
            transition: all .2s;
        }

        &:hover,
        &:active {
            color: $color-primary;
            box-shadow: 0 1rem 2rem rgba($color-black, .4);
            transform: rotate(5deg) scale(1.3);
        }
    }

    &__copyright {
        border-top: 1px solid $color-grey-dark;
        padding-top: 2rem;
        width: 80%;
        float: right;

        @include respond(tab-port) {
            width: 100%;
            float: none;
        }
    }
}
</style>