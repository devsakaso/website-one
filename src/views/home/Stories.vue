<template>
  <!-- 背景ビデオ -->
  <div class="bg-video">
    <video class="bg-video__content" autoplay muted loop>
      <source v-for="(video, index) in storiesData.videos" :key="index" :src="require('@/assets/img/' + video.src)" :type="video.type">
      {{ storiesData.videoError }}
    </video>
  </div>

  <!-- タイトル -->
  <div class="u-center-text u-margin-bottom-big">
    <h2 class="heading-secondary">
        {{ storiesData.title }}
    </h2>
  </div>

  <!-- レビュー -->
  <div class="row" v-for="story in storiesData.stories" :key="story">
    <div class="story">
      <figure class="story__shape">
        <img :src="require('@/assets/img/' + story.image)" alt="Person on a tour" class="story__img">
        <figcaption class="story__caption">{{ story.name }}</figcaption>
      </figure>
      <div class="story__text">
        <h3 class="heading-tertiary u-margin-bottom-small">{{ story.subtitle }}</h3>
        <p>{{ story.text }}</p>
      </div>
    </div>
  </div>

  <!-- ボタン -->
  <div class="u-center-text u-margin-top-huge">
    <a href="#book" class="btn-text">{{ storiesData.button }} &rarr;</a>
  </div>
</template>

<script>
export default {
  setup() {
    const storiesData = {
      title: 'みんなのリアルな留学体験',
      videos: [
                {
                  src: 'video.mp4',
                  format: 'video/mp4'
                },
                {
                  src: 'video.webm',
                  format: 'video/webm'
                },
              ],
      videoError: '現在のブラウザではこの動画はサポートされていません。',
      stories: [
                  {
                    image: 'stories-1.jpg',
                    name: 'Hanako Yamada',
                    subtitle: '気づいたら、自然と聞きとれるように',
                    text: 'Lorem ipsum dolor sit amet consectetur adipisicing elit. Aperiam, ipsum sapiente aspernatur libero repellat quis consequatur ducimus quam nisi exercitationem omnis earum qui. Aperiam, ipsum sapiente aspernatur libero repellat quis consequatur ducimus quam nisi exercitationem omnis earum qui.'
                  },
                  {
                    image: 'stories-2.jpg',
                    name: 'Taro Sasaki',
                    subtitle: '想像をはるかに超えた異文化の体験をした',
                    text: 'Lorem ipsum dolor sit amet consectetur adipisicing elit. Aperiam, ipsum sapiente aspernatur libero repellat quis consequatur ducimus quam nisi exercitationem omnis earum qui. Aperiam, ipsum sapiente aspernatur libero repellat quis consequatur ducimus quam nisi exercitationem omnis earum qui.'
                  },
                ],
        button: '詳しくみる'
    }

    return {
      storiesData
    }
  },
}
</script>

<style lang="scss" scoped>
.story {
    width: 75%;
    margin: 0 auto;
    box-shadow: 0 3rem 6rem rgba($color-black, .1);
    background-color: rgba($color-white, .6);
    border-radius: 3px;
    padding: 6rem;
    padding-left: 9rem;
    font-size: $default-font-size;
    transform: skewX(-12deg);

    @include respond(tab-port) {
        width: 100%;
        padding: 4rem;
        padding-left: 7rem;
    }

    @include respond(phone) {
        transform: skewX(0);
    }

    &__shape {
        width: 15rem;
        height: 15rem;
        float: left;
        transform: translateX(-3rem) skewX(12deg);
        position: relative;
        overflow: hidden;
        border-radius: 50%;

        @supports (clip-path: polygon(0 0)) or (-webkit-clip-path: polygon(0 0)) {
            -webkit-clip-path: circle(50% at 50% 50%);
            clip-path: circle(50% at 50% 50%);
            -webkit-shape-outside: circle(50% at 50% 50%);
            shape-outside: circle(50% at 50% 50%);
            border-radius: none;
        }

        @include respond(phone) {
            transform: translateX(-3rem) skewX(0);
        }
    }

    &__img {
        height: 100%;
        transform: translateX(-4rem) scale(1.4);
        backface-visibility: hidden;
        transition: all .5s;
    }

    &__text {
        transform: skewX(12deg);

        @include respond(phone) {
            transform: skewX(0);
        }
    }

    &__caption {
        position: absolute;
        top: 50%;
        left: 50%;
        transform: translate(-50%, 20%);
        color: $color-white;
        text-transform: uppercase;
        font-size: 1.7rem;
        text-align: center;
        opacity: 0;
        transition: all .5s;
        backface-visibility: hidden;
    }

    &:hover &__caption {
        opacity: 1;
        transform: translate(-50%, -50%);
    }

    &:hover &__img {
        transform: translateX(-4rem) scale(1);
        filter: blur(3px) brightness(80%);
    }
}
</style>