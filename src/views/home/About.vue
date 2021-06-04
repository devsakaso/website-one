<template>
  <!-- タイトル -->
  <div class="u-center-text u-margin-bottom-big">
    <h2 class="heading-secondary">
        {{ aboutData.title }}
    </h2>
  </div>

  <div class="row">
    <!-- テキスト -->
    <div class="col-1-of-2">
      <div class="u-margin-bottom-medium" v-for="item in aboutData.texts" :key="item">

        <h3 class="heading-tertiary u-margin-bottom-small">{{ item.subtitle }}</h3>
        <p class="paragraph">
            {{ item.paragraph }}
        </p>
      </div>

      <!-- ボタン -->
      <a href="#book" class="btn-text">{{ aboutData.button }} &rarr;</a>
    </div>
    
    <!-- 画像 -->
    <div class="col-1-of-2">
      <div class="composition">

          <img
            v-for="image in aboutData.images"
            :key="image.id"
            :src="require('@/assets/img/' + image.src)"
            :alt="image.alt"
            class="composition__photo"
            :class="'composition__photo--p' + image.id">
         
      </div>
    </div>
  </div>
</template>

<script>
export default {
  setup() {
    const aboutData = {
    title: '海外で自分を見つめ直す',
    button: '詳しくみる',
    texts: [
              {
                subtitle: '留学は、勉強だけじゃない',
                paragraph: 'Lorem ipsum dolor sit amet consectetur adipisicing elit. Aperiam, ipsum sapiente aspernatur libero repellat quis consequatur ducimus quam nisi exercitationem omnis earum qui.'
              },
              {
                subtitle: 'アクティビティも充実',
                paragraph: 'Lorem ipsum dolor sit amet consectetur adipisicing elit. Aperiam, ipsum sapiente aspernatur libero repellat quis consequatur ducimus quam nisi exercitationem omnis earum qui.'
              }
            ],
    images: [
              {
                src: 'about-1.jpg',
                alt: 'Photo1',
                id: 1,
              },
              {
                src: 'about-2.jpg',
                alt: 'Photo2',
                id: 2,
              },
              {
                src: 'about-3.jpg',
                alt: 'Photo3',
                id: 3,
              }
            ]
    }

    return {
      aboutData
    }
  },
}
</script>

<style lang="scss" scoped>
.composition {
    position: relative;

    &__photo {
        width: 55%;
        box-shadow: 0 1.5rem 4rem rgba($color-black, .4);
        border-radius: 2px;
        position: absolute;
        z-index: 10;
        transition: all .2s;
        outline-offset: 2rem;

        @include respond(tab-port) {
            float: left;
            position: relative;
            width: 33.33333333%;
            box-shadow: 0 1.5rem 3rem rgba($color-black, .2);
        }

        &--p1 {
            left: 0;
            top: -2rem;

            @include respond(tab-port)  {
                top: 0;
                transform: scale(1.2);
            }
        }

        &--p2 {
            right: 0;
            top: 2rem;

            @include respond(tab-port)  {
                top: -1rem;
                transform: scale(1.3);
                z-index: 100;
            }
        }

        &--p3 {
            left: 20%;
            top: 10rem;

            @include respond(tab-port)  {
                top: 1rem;
                left: 0;
                transform: scale(1.1);
            }
        }

        &:hover {
            outline: 1.5rem solid $color-primary;
            transform: scale(1.05) translateY(-.5rem);
            box-shadow: 0 2.5rem 4rem rgba($color-black, .5);
            z-index: 20;
        }

    }

    &:hover &__photo:not(:hover) {
        transform: scale(.95);
    }
}
</style>
