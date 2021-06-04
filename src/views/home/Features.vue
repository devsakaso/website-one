<template>
    <div class="row">
      <div v-for="item in featuresData" :key="item.icon" :class="`col-1-of-${featuresData.length}`">
        <div class="feature-box">
          <i class="feature-box__icon" :class="item.icon"></i>
          <h3 class="heading-tertiary u-margin-bottom-small">{{ item.subtitle }}</h3>
          <p class="feature-box__text">
            {{ item.text }}
          </p>
        </div>
      </div>
  </div>
</template>

<script>
export default {
  setup() {
    const featuresData = [
      {
        icon: 'bx bx-world',
        subtitle: '海外で暮らす',
        text: 'Lorem ipsum dolor sit amet consectetur adipisicing elit. Aperiam, ipsum sapiente aspernatur.',
      },
      {
        icon: 'bx bxs-store',
        subtitle: '仕事を体験する',
        text: 'Lorem ipsum dolor sit amet consectetur adipisicing elit. Aperiam, ipsum sapiente aspernatur.',
      },
      {
        icon: 'bx bxs-pen',
        subtitle: '語学を学ぶ',
        text: 'Lorem ipsum dolor sit amet consectetur adipisicing elit. Aperiam, ipsum sapiente aspernatur.',
      },
      {
        icon: 'bx bxs-building',
        subtitle: 'インターンシップ',
        text: 'Lorem ipsum dolor sit amet consectetur adipisicing elit. Aperiam, ipsum sapiente aspernatur.',
      },
    ]
    return {
      featuresData,
    }
  },
}
</script>

<style lang="scss" scoped>
.feature-box {
    background-color: rgba($color-white, .8);
    font-size: 1.5rem;
    padding: 2.5rem;
    text-align: center;
    border-radius: 3px;
    box-shadow: 0 1.5rem 4rem rgba($color-black, .15);
    transition: transform .3s;

    @include respond(tab-port) {
        padding: 2rem;
    }

    &__icon {
        font-size: 6rem;
        margin-bottom: .5rem;
        display: inline-block;
        background-image: linear-gradient(to right, $color-primary-light, $color-primary-dark);
        -webkit-background-clip: text;
        color: transparent;

        @include respond(tab-port) {
            margin-bottom: 0;
        }
    }

    &:hover {
        transform: translateY(-1.5rem) scale(1.03);
    }
}
</style>