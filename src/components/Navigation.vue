<template>
  <div class="navigation">
    <!-- ボタン -->
    <div class="navigation__button" @click="showMenu = !showMenu" :class="{ 'menu-active' : showMenu }">
        <span class="navigation__icon">&nbsp;</span>
    </div>

    <!-- メニュー -->
    <div :class="{ 'show-menu' : showMenu }">
      <!-- 背景 -->
      <div class="navigation__background">&nbsp;</div>
      <!-- ナブ -->
      <nav class="navigation__nav">
          <ul class="navigation__list">
              <li class="navigation__item" v-for="item in items" :key="item.id">
                <a :href="item.link" class="navigation__link"  @click="showMenu = !showMenu">
                  <span>{{ item.id }}</span>
                  {{ item.text }}
                </a>
              </li>
          </ul>
      </nav>
    </div>
  </div>
</template>

<script>
import { ref } from 'vue'

export default {
  setup() {

    const items = ref([
      { id:1, text:'サービスについて', link: '#about' },
      { id:2, text:'サービスの特徴', link: '#features' },
      { id:3, text:'人気のプラン', link: '#tours' },
      { id:4, text:'ストーリー', link: '#stories' },
      { id:5, text:'無料で資料請求', link: '#book' },
    ])

    const showMenu = ref(false)

    return {
      items,
      showMenu,
    }
  }
}
</script>

<style lang="scss" scoped>
.navigation {
  // ボタン
    &__button {
        background-color: $color-white;
        height: 7rem;
        width: 7rem;
        position: fixed;
        top: 6rem;
        right: 6rem;
        border-radius: 50%;
        z-index: 2000;
        box-shadow: 0 1rem 3rem rgba($color-black, .1);
        text-align: center;
        cursor: pointer;

        @include respond(tab-port) {
            top: 4rem;
            right: 4rem;
        }

        @include respond(phone) {
            top: 3rem;
            right: 3rem;
        }
    }
    // 背景
    &__background {
        height: 6rem;
        width: 6rem;
        border-radius: 50%;
        position: fixed;
        top: 6.5rem;
        right: 6.5rem;
        background-image: radial-gradient($color-primary-light, $color-primary-dark);
        z-index: 1000;
        transition: transform .8s cubic-bezier(0.86, 0, 0.07, 1);

        @include respond(tab-port) {
            top: 4.5rem;
            right: 4.5rem;
        }

        @include respond(phone) {
            top: 3.5rem;
            right: 3.5rem;
        }
    }
    // ナブ
    &__nav {
        height: 100vh;
        position: fixed;
        top: 0;
        left: 0;
        z-index: 1500;

        opacity: 0;
        width: 0;
        transition: all .8s cubic-bezier(0.68, -0.55, 0.265, 1.55);
    }

    //リスト
    &__list {
        position: absolute;
        top: 50%;
        left: 50%;
        transform: translate(-50%,-50%);
        list-style: none;
        text-align: center;
        width: 100%;
    }
    // リストアイテム
    &__item {
        margin: 1rem;
    }
    // ナブリンク
    &__link {
        &:link,
        &:visited {
            display: inline-block;
            font-size: 3rem;
            font-weight: 300;
            padding: 1rem 2rem;
            color: $color-white;
            text-decoration: none;
            text-transform: uppercase;
            background-image: linear-gradient(120deg, transparent 0%, transparent 50%, $color-white 50%);
            background-size: 220%;
            transition: all .4s;
            transform: translateX(-300%); //画面外へ

            span {
                margin-right: 1.5rem;
                display: inline-block;
            }
        }
        
        &:hover,
        &:active {
            background-position: 100%;
            color: $color-primary;
        }
    }


    //メニューが開くときのファンクション
    .show-menu &__background {
      transform: scale(80);
    }

    .show-menu &__nav {
        opacity: 1;
        width: 100%;
    }

    .show-menu &__link {
      &:link,
      &:visited {
          transform: translateX(0);
      }
      &:hover,
      &:active {
          transform: translateX(1rem);
      }
    }


    //アイコン
    &__icon {
        position: relative;
        margin-top: 3.5rem;

        &,
        &::before,
        &::after {
            width: 3rem;
            height: 2px;
            background-color: $color-grey-dark-3;
            display: inline-block;
        }

        &::before,
        &::after {
            content: "";
            position: absolute;
            left: 0;
            transition: all .2s;
        }

        &::before { top: -.8rem; }
        &::after { top: .8rem; }
    }
    
    // ホバー時のアイコン状態
    &__button:hover &__icon::before {
        top: -1rem;
    }

    &__button:hover &__icon::after {
        top: 1rem;
    }

    // メニューが開いているときのアイコン状態
    &__button.menu-active &__icon {
        background-color: transparent;
    }

    &__button.menu-active &__icon::before {
        top: 0;
        transform: rotate(135deg);
    }

    &__button.menu-active &__icon::after {
        top: 0;
        transform: rotate(-135deg);
    }
}
</style>