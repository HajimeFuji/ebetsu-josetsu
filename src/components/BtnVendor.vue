<template>
  <div @click="onClick">
    <div class="view" v-if="!isMini">
      <div class="view__1">
        <p class="view__text">{{title}}</p>
        <div class="resultbox">
          <img v-bind:src="require(`@/assets/${iconPath}`)" alt="" class="view__logo">
          <div class="result">
            <p class="result__data">{{vendorCount}}</p>
            <p class="result__output">業者</p>
          </div>
        </div>
      </div>
    </div>
    <div class="view__b" v-if="isMini">
      <div class="view__b__2">
        <p class="view__text__2">{{title}}</p>
        <!-- <img v-bind:src="require(`@/assets/${iconPath}`)" alt="" class="view__logo-2"> -->
        <div class="resultbox-2">
          <img v-bind:src="require(`@/assets/${iconPath}`)" alt="" class="view__logo-2">
          <div class="result-2">
            <p class="result__data-2">{{vendorCount}}</p>
            <p class="result__output-2">業者</p>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
  export default {
    props: {
      title: {type: String, required: true},
      iconPath: {type: String, required: true},
      vendorCount: {type: Number, required: true},
      isMini: Boolean,
      onClick: {type: Function, required: true}
    }
  }
</script>


<style lang="scss" scoped>
$breakpoint: (
  sp:'screen and (max-width:599px)',
  tab:'screen and (max-width:1024px)',
  pc:'screen and (min-width:1025px)',
);

@mixin mq($size) {
  @media #{map-get($breakpoint, $size)} {
    @content;
  }
}

* {
  margin: 0;
  padding: 0;
}

.view {
  background-color: #F4CB05;
  border-radius: 15px;
  box-shadow: 4px 4px 0px #FFFFFF;
  cursor: pointer;
  width: 505px;
  height: 240px;
  @include mq(sp) {
      width: calc(100vw * 0.85);
      aspect-ratio: 0.5;
    }
  &__1 {
    display: flex;
    flex-flow: column;
    justify-content: space-between;
    width: 100%;
    height: 100%;
  }
  &__text {
    font-family: Hiragino sans;
    font-size: 28px;
    font-weight: 400;
    letter-spacing: 0.42em;
    text-align: left;
    margin-top: 40px;
    margin-left: 40px;
    @include mq(sp) {
      margin-left: 8%;
    }
    &__2 {
      font-size: 22px;
      margin-top: 40px;
      margin-left: 20px;
      @include mq(sp) {
        font-size: 20px;
        letter-spacing: normal;
        margin-top: 43px;
        margin-left: 2%;
      }
    }
  }

  &__logo {
    height: 54px;
    margin-left: 40px;

    @include mq(sp) {
      height: 46px;
    }

    &-2 {
      height: 35px;
    }
  }
}
.view__b {
  background-color: #F4CB05;
  border-radius: 15px;
  box-shadow: 4px 4px 0px #FFFFFF;
  cursor: pointer;
  width: 240px;
  height: 240px;
  @include mq(sp) {
    width: calc(100vw * 0.4);
    aspect-ratio: 1;
  }
  &__2 {
    display: flex;
    flex-flow: column;
    justify-content: space-between;
    align-items: center;
    width: 100%;
    height: 100%;
  }
}

.resultbox {
  display: flex;
  width: 95%;
  justify-content: space-between;
  margin-bottom: 20px;

  &-2 {
    flex-flow: column;
    align-items: center;
    margin-bottom: 20px;
  }
}

.resultbox {
  display: flex;
  width: 95%;
  justify-content: space-between;
  margin-bottom: 20px;

  &-2 {
    flex-flow: column;
    align-items: center;
    margin-bottom: 20px;
  }
}

.result {
  display: flex;
  align-items: baseline;
  &__data {
    font-family: Hiragino sans;
    font-size: 63px;
    font-weight: 400;
    letter-spacing: 0.06em;
    margin-right: 42px;

    @include mq(sp) {
      font-size: 54px;
      font-weight: 500;
      margin-right: 20px;
    }

    &-2 {
      font-size: 46px;
      // margin-right: 24px;

      @include mq(sp) {
        font-size: 42px;
        font-weight: 500;
      }
    }
  }

  &__output {
    font-family: Hiragino sans;
    font-size: 24px;
    font-weight: 400;
    letter-spacing: 0.22em;
    @include mq(sp) {
      font-size: 22px;
    }

    &-2 {
      font-size: 18px;
    }
  }
}

</style>
