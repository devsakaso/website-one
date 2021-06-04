<template>
  <div class="u-center-text u-margin-bottom-big">
    <!-- タイトル -->
    <h2 class="heading-secondary">
        {{ toursData.title }}
    </h2>
  </div>

  <div class="row">
    <div class="col-1-of-3" v-for="card in toursData.cards" :key="card.id">
      <div class="card">
        <!-- カードフロントサイド -->
        <div class="card__side card__side--front">
          <div class="card__picture" :class="'card__picture--' + card.id">
            &nbsp;
          </div>
          <h4 class="card__heading">
            <span class="card__heading-span" :class="'card__heading-span--' + card.id">{{ card.subtitle }}</span>
          </h4>
          <div class="card__details">
            <ul>
              <li v-for="item in card.details" :key="item">{{ item }}</li>
            </ul>
          </div>
        </div>
        <!-- カードバックサイド -->
        <div class="card__side card__side--back" :class="'card__side--back-' + card.id">
          <div class="card__cta">
            <div class="card__price-box">
              <p class="card__price-only">Only</p>
              <p class="card__price-value">{{ card.price }}<span>万円~</span></p>
            </div>
            <a class="btn btn--white" @click="openPopup">{{ toursData.cardButton }}</a>
          </div>
        </div>
      </div>
    </div>
  </div>

  <!-- ボタン -->
  <div class="u-center-text u-margin-top-huge">
      <a href="#" class="btn btn--green" @click="openPopup">{{ toursData.button }}</a>
  </div>

  <!-- ポップアップ -->
  <transition name="card-popup" appear>
  <Popup @close="closePopup" v-show="popup" :class="{'is-active': popup}"/>
  </transition>

</template>

<script>
import Popup from '@/components/Popup.vue'

import { ref } from 'vue'
export default {
  components: {
    Popup
  },
  setup() {
    const toursData = {
      title: '最も人気のプラン',
      button: 'パンフレットをゲットする',
      cardButton: '詳しく見る',
      cards: [
        {
          id: 1,
          subtitle: '短期留学',
          details:[
            '2~16週',
            '滞在中は24時間サポート',
            '上達保証システム',
            '公的機関による認可',
            '認可ホストファミリーの紹介',
          ],
          price: '29',
        },
        {
          id: 2,
          subtitle: 'ワーキングホリデー',
          details:[
            '1ヶ月~1年',
            '滞在中は24時間サポート',
            '上達保証システム',
            '公的機関による認可',
            '認可ホストファミリーの紹介',
          ],
          price: '59',
        },
        {
          id: 3,
          subtitle: '長期留学',
          details:[
            '1年~',
            '滞在中は24時間サポート',
            '上達保証システム',
            '公的機関による認可',
            '認可ホストファミリーの紹介',
          ],
          price: '120',
        },
      ]
    }

    const popup = ref(false)
    const openPopup = () => {
      popup.value = true
      console.log('popup');
    }
    const closePopup = () => {
      console.log('close');
      popup.value = false
    }

    return {
      toursData,
      popup,
      openPopup,
      closePopup
    }
  },
}
</script>


<style lang="scss" scoped>
.card {

  // FUNCTIONALITY
  perspective: 150rem;
  -moz-perspective: 150rem;
  position: relative;
  height: 52rem;
  
  &__side {
    height: 52rem;
    transition: all .8s ease;
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    -webkit-backface-visibility: hidden;
    backface-visibility: hidden;
    border-radius: 3px;
    overflow: hidden;
    box-shadow: 0 1.5rem 4rem rgba($color-black, .15);

    &--front {
      background-color: $color-white;
    }

    // バックサイドに切り替わったときのrotate
    &--back {
      transform: rotateY(180deg);

      &-1 {
        background-image: linear-gradient(to right bottom, $color-secondary-light, $color-secondary-dark);
      }

      &-2 {
        background-image: linear-gradient(to right bottom, $color-primary-light, $color-primary-dark);
      }

      &-3 {
        background-image: linear-gradient(to right bottom, $color-tertiary-light, $color-tertiary-dark);
      }
    }
  }

  // フロントサイドのrotate
  &:hover &__side--front {
      transform: rotateY(-180deg);
  }
  // フロントサイドのrotateのときにバックサイドのrotateも同時に行う
  &:hover &__side--back {
      transform: rotateY(0);
  }


  // フロントサイド
  &__picture {
    background-size: cover;
    height: 23rem;
    background-blend-mode: screen;
    -webkit-clip-path: polygon(0 0, 100% 0, 100% 85%, 0 100%);
    clip-path: polygon(0 0, 100% 0, 100% 85%, 0 100%);
    border-top-left-radius: 3px;
    border-top-right-radius: 3px;
    
    &--1 {
      background-image: linear-gradient(to right bottom, $color-secondary-light, $color-secondary-dark), 
      url(~@/assets/img/tours-1.jpg);
    }

    &--2 {
      background-image: linear-gradient(to right bottom, $color-primary-light, $color-primary-dark), 
      url(~@/assets/img/tours-2.jpg);
    }

    &--3 {
      background-image: linear-gradient(to right bottom, $color-tertiary-light, $color-tertiary-dark), 
      url(~@/assets/img/tours-3.jpg);
    }
  }

  &__heading {
      font-size: 2.8rem;
      font-weight: 300;
      text-transform: uppercase;
      text-align: right;
      color: $color-white;
      position: absolute;
      top: 12rem;
      right: 2rem;
      width: 75%;
  }

  &__heading-span {
    padding: 1rem 1.5rem;
    -webkit-box-decoration-break: clone;
    box-decoration-break: clone;

    &--1 {
      background-image: linear-gradient(to right bottom, 
      rgba($color-secondary-light, .85), 
      rgba($color-secondary-dark, .85));
    }

    &--2 {
      background-image: linear-gradient(to right bottom, 
      rgba($color-primary-light, .85), 
      rgba($color-primary-dark, .85));
    }

    &--3 {
      background-image: linear-gradient(to right bottom, 
      rgba($color-tertiary-light, .85), 
      rgba($color-tertiary-dark, .85));
    }
  }

  &__details {
    padding: 3rem;

    ul {
      list-style: none;
      width: 80%;
      margin: 0 auto;

      li {
        text-align: center;
        font-size: 1.5rem;
        padding: 1rem;

        &:not(:last-child) {
          border-bottom: 1px solid $color-grey-light-2;
        }
      }
    }
  }

  // バックサイド
  &__cta {
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    width: 90%;
    text-align: center;
  }

  &__price-box {
    text-align: center;
    color: $color-white;
    margin-bottom: 8rem;
  }

  &__price-only {
    font-size: 1.4rem;
    text-transform: uppercase;
  }

  &__price-value {
    font-size: 6rem;
    font-weight: 500;
    & span {
    margin-left: 1rem;
       font-size: 2.5rem;
       font-weight: 100;   
    }
  }




  //@include respond(tab-port) {
  @media only screen and (max-width: 56.25em),
          only screen and (hover: none) {

    height: auto;
    border-radius: 3px;
    background-color: $color-white;
    box-shadow: 0 1.5rem 4rem rgba($color-black, .15);
    
    // ホバーできないので下にくっつける
    &__side {
      height: auto;
      position: relative;
      box-shadow: none;

      &--back {
        transform: rotateY(0);
        clip-path: polygon(0 15%, 100% 0, 100% 100%, 0% 100%);
      }
    }
  
    &:hover &__side--front {
      transform: rotateY(0);
    }


    &__details {
      padding: 1rem 3rem;
    }

    // FRONT SIDE STYLING
    &__cta {
      position: relative;
      top: 0%;
      left: 0;
      transform: translate(0);
      width: 100%;
      padding: 7rem 4rem 4rem 4rem;
    }

    &__price-box {
      margin-bottom: 3rem;
    }

    &__price-value {
      font-size: 4rem;
    }
  }

  // ポップアップのアニメーション
  &-popup {
    &-enter-active {
      animation: open .3s ease-in-out;
    }
    &-leave-active {
      animation: close .3s ease-in-out;
    }
  }
  @keyframes open {
    from { 
      opacity: 0;
      transform: scale(.25);
    }
    to { 
      opacity: 1;
      transform: scale(1);
    }
  }
  @keyframes close {
    from { 
      opacity: 1;
      transform: scale(1);
    }
    to { 
      opacity: 0;
      transform: scale(0.25);
    }
  }
}
</style>