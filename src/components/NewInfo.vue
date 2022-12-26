<template>
  <div class="news">
    <p class="news__title">除雪新着情報</p>
    <p class="news__date">{{ date }}</p>
    <p class="news__msg">{{ msg }}</p>
  </div>
</template>

<script>
import { DateTime } from 'luxon'

export default {
  data() {
    return {
      msg: '',
      date: ''
    }
  },
  methods: {
    async getInfo() {
      const response = await fetch('https://api.ebetsu-data.com/josetsu/info', {
        headers: {
          cache: 'no-store',
          'Content-Type': 'application/json'
        },
      });

      const info = await response.json()

      this.msg = info.contents
      this.date = DateTime.fromISO(info.date).setLocale('ja').toFormat('yyyy/MM/dd HH:mm');
    }
  },
  mounted() {
    this.getInfo()
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

.news {
  width: 30%;
  background-color: #FFFFFF;
  margin-right: 70px;
  padding: 16px;

  @include mq(tab) {
    width: 40%;
  }

  @include mq(sp) {
    display: block;
    width: 90%;
    margin: 140px auto auto;
    border-radius: 10px;
  }

  &__title {
    font-family: Hiragino sans;
    font-size: 24px;
    margin: 0;
    letter-spacing: 0.79em;
    padding-top: 10px;
    padding-bottom: 10px;

    @include mq(sp) {
      letter-spacing: 0.35em;
    }
  }

  &__date {
    font-family: Hiragino sans;
    font-size: 16px;
    margin: 0;
    margin-bottom: 4px;
    text-align: left;
    color: rgba($color: #000000, $alpha: 0.7);

    @include mq(sp) {
      margin: initial;
    }
  }

  &__msg {
    font-family: Hiragino sans;
    font-size: 16px;
    letter-spacing: 0.35em;
    margin: 0;
    padding-bottom: 10px;
    text-align: left;
    white-space: pre-line;

    @include mq(sp) {
      margin: initial;
    }
  }

}
</style>