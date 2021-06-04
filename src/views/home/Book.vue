<template>
  <div class="row">
    <div class="book">
      <div class="book__form">
        <!-- フォーム -->
        <form action="#" class="form">
          <!-- タイトル -->
          <div class="u-margin-bottom-medium">
            <h2 class="heading-secondary">
                {{ bookData.title }}
            </h2>
          </div>

          <!-- インプット -->
          <div class="form__group" v-for="item in bookData.inputs" :key="item">
            <input :type="item.type" class="form__input" :placeholder="item.text" :id="item.id" required>
            <label :for="item.id" class="form__label">{{ item.text }}</label>
          </div>

          <!-- ラジオボタン -->
          <div class="form__group u-margin-bottom-medium">
            <div class="form__radio-group" v-for="item in bookData.radioButtons" :key="item.id">
              <input type="radio" class="form__radio-input" :id="item.id" name="plan">
              <label :for="item.id" class="form__radio-label">
                <span class="form__radio-button"></span>
                {{ item.text }}
              </label>
            </div>

          </div>

          <!-- ボタン -->
          <div class="form__group">
            <button class="btn btn--green"> {{ bookData.button }} &rarr;</button>
          </div>
        </form>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  setup() {
    const bookData = {
    title: 'パンフレットはこちら',
    button: '無料で請求する',
    inputs: [
              {
                type: 'text',
                id: 'name',
                text: 'お名前'
              },
              {
                type: 'email',
                id: 'email',
                text: 'メールアドレス'
              },
            ],
    radioButtons: [
                    {
                      id: 'short',
                      text: '短期留学'
                    },
                    {
                      id: 'long',
                      text: '長期留学'
                    },
                    {
                      id: 'working',
                      text: 'ワーキングホリデー'
                    },
                    {
                      id: 'undecided',
                      text: 'まだ決めていない'
                    },
                   ]
    }

    return {
      bookData
    }
  },
}
</script>

<style lang="scss" scoped>
.form {
    &__group:not(:last-child) {
        margin-bottom: 2rem;
    }

    &__input {
        font-size: 1.5rem;
        font-family: inherit;
        color: inherit;
        padding: 1.5rem 2rem;
        border-radius: 2px;
        background-color: rgba($color-white, .5);
        border: none;
        border-bottom: 3px solid transparent;
        width: 90%;
        display: block;
        transition: all .3s;

        @include respond(tab-port) {
            width: 100%;
        }

        &:focus {
            outline: none;
            box-shadow: 0 1rem 2rem rgba($color-black, .1);
            border-bottom: 3px solid $color-primary;
        }

        &:focus:invalid {
            border-bottom: 3px solid $color-secondary-dark;
        }

        &::-webkit-input-placeholder {
            color: $color-grey-dark-2;
        }
    }


    &__label {
        font-size: 1.2rem;
        font-weight: 700;
        margin-left: 2rem;
        margin-top: .7rem;
        display: block;
        transition: all .3s;
    }

    &__input:placeholder-shown + &__label {
        opacity: 0;
        visibility: hidden;
        transform: translateY(-4rem);
    }


    &__radio-group {
        width: 49%;
        display: inline-block;

        @include respond(tab-port) {
            width: 100%;
            margin-bottom: 2rem;
        }
    }

    &__radio-input {
        display: none;
    }
    
    &__radio-label {
        font-size: $default-font-size;
        cursor: pointer;
        position: relative;
        padding-left: 4.5rem;
    }

    &__radio-button {
        height: 3rem;
        width: 3rem;
        border: 5px solid $color-primary;
        border-radius: 50%;
        display: inline-block;
        position: absolute;
        left: 0;
        top: -.4rem;

        &::after {
            content: "";
            display: block;
            height: 1.3rem;
            width: 1.3rem;
            border-radius: 50%;
            position: absolute;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            background-color: $color-primary;
            opacity: 0;
            transition: opacity .2s;
        }
    }

    &__radio-input:checked ~ &__radio-label &__radio-button::after {
        opacity: 1;
    }
}

</style>