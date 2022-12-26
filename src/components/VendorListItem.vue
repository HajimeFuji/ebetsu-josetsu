<template>
  <div>
    <div class="companyinfo">
      <div class="companyinfo__name">
        <p>{{vendor.company_name}}</p>
      </div>
      <div class="companyinfo__post">
        <p>〒{{vendor.zip_code}}</p>
      </div>
      <div class="companyinfo__address">
        <p>{{vendor.address}}</p>
      </div>
      <div class="companyinfo-phonebox">
        <img src="../assets/phone.png" alt="" class="companyinfo__img">
        <div class="companyinfo__phone">
          <a v-bind:href='`tel:${vendor.phone_number.replaceAll("-", "")}`' v-if="isMobile">
            {{vendor.phone_number}}
          </a>
          <p v-else>{{vendor.phone_number}}</p>
        </div>
      </div>
    </div>
    <div v-bind:class="menuClass">
      <label>{{isOpen ? '－詳細' : '＋詳細'}}
        <input type="checkbox" v-on:change="changeMenuState" v-model="isOpen">
      </label>
      <ul>
        <div class="detailbox">
          <li class="detail">
            <div class="detail__item">
              <img src="../assets/door_y.png" alt="" class="detail__img">
              <p class="detail__title">排雪</p>
            </div>
            <p class="detail__text">{{vendor.aisle_snow_remove ? vendor.aisle_snow_remove : '実施していません'}}</p>
          </li>
          <li class="detail">
            <div class="detail__item">
              <img src="../assets/house_y.png" alt="" class="detail__img">
              <p class="detail__title">間口</p>
            </div>
            <p class="detail__text">{{vendor.misplaced_snow ? vendor.misplaced_snow : '実施していません'}}</p>
          </li>
          <li class="detail">
            <div class="detail__item">
              <img src="../assets/roof_y.png" alt="" class="detail__img">
              <p class="detail__title">屋根</p>
            </div>
            <p class="detail__text">{{vendor.roof_snow_remove ? vendor.roof_snow_remove : '実施していません'}}</p>
          </li>
          <li class="detail">
            <div class="detail__item">
              <img src="../assets/door_y.png" alt="" class="detail__img">
              <p class="detail__title">玄関・通路</p>
            </div>
            <p class="detail__text">{{vendor.remove_snow ? vendor.remove_snow : '実施していません'}}</p>
          </li>
        </div>
        <div class="detail-note">
          <p>{{vendor.overview}}</p>
        </div>
      </ul>
    </div>

  </div>
</template>


<script>
import { is } from '@babel/types';

  export default {
    props: {
      vendor:  Object
    },
    methods: {
      changeMenuState() {
        if (this.isOpen) {
          this.menuClass = {
            'menu': true,
            'menu_open': true,
            'menu_close': false,
          }
        } else {
          this.menuClass = {
            'menu': true,
            'menu_open': false,
            'menu_close': true,
          }
        }
      }
    },
    data() {
      return {
        isOpen: false,
        menuClass: {
          'menu': true,
          'menu_open': false,
          'menu_close': true,
        },
        isMobile: navigator.userAgent.match(/iPhone|Android.+Mobile/)
      }
    },
  }
</script>

<style lang="scss" scoped>
$breakpoint:(
    sp:'screen and (max-width:599px)',
    tab:'screen and (max-width:1024px)',
    pc:'screen and (min-width:1025px)',
);

@mixin mq($size) {
    @media #{map-get($breakpoint, $size)}{
        @content;
    }
}

*{
    margin: 0;
    padding: 0;
}
.companyinfo {
  display: flex;
  padding: 0 16px;
  width: 95%;
  align-items: baseline;
  margin-top: 24px;
  margin-bottom: 24px;
  font-family: Hiragino sans;
  font-weight: 300;
  letter-spacing: 0.22em;
  justify-content: space-between;
  flex-wrap: wrap;
  @include mq(sp){
      display: flex;
      flex-flow: column;
      align-items: flex-start;
      justify-content: center;
      width: 100%;
      margin: 40px 0 0 0;
      padding: initial;
      letter-spacing: normal;
  }
  &__name {
      font-size: 32px;
      flex-basis: 30%;
      text-align: left;
      @include mq(sp) {
          margin: initial;
          margin-bottom: 16px;
      }
  }
  &__post {
      font-size: 16px;
      flex-basis: 10%;
      text-align: left;
      @include mq(sp) {
          margin: initial;
          margin-bottom: 6px;
      }
  }
  &__address {
      font-size: 24px;
      flex-basis: 40%;
      text-align: left;
      @include mq(sp) {
          margin: initial;
          margin-bottom: 12px;
      }
  }
  &-phonebox {
      display: flex;
      flex-basis: 20%;
      text-align: left;
      align-items: baseline;
      @include mq(sp) {
          // margin-bottom: 40px;
      }
  }
  &__img {
      width: 24px;
      height: 24px;
      margin-right: 20px;
  }
  &__phone {
      font-size: 28px;
  }
}

.menu {
    padding: 0 16px;
    @include mq(sp) {
      padding: initial;
    }
}
/* チェックボックスは非表示にする（内部的な Off/On の機能だけ利用する） */
.menu input {
    display: none;
}
/* 開いた状態のサブメニュー */
.menu_open {
  ul {
    display: block;
  }
}

.menu_close {
  ul {
    display: none;
    /* 下記は開閉によらず共通の設定 */
    // background: #FFFFFF;
    // border-radius: 20px;
    // width: 100%;
    // height: 418px;
    list-style: none;
    margin: 0;
    padding: 1rem;
  }
}

/* 親項目の装飾 */
.menu label {
    display: flex;
    align-items: center;
    justify-content: center;
    width: 134px;
    height: 40px;
    margin-bottom: 20px;
    padding: 0.5rem;
    background: #FFFFFF;
    border: 1px solid #707070;
    border-radius: 10px;
    font-family: Hiragino sans;
    font-size: 20px;
    letter-spacing: 0.75em;
    cursor: pointer;
    @include mq(sp) {
        width: 103px;
        height: 33px;
        border-radius: 0;
        font-size: 16px;
        margin: 0 0 0 auto;
        padding: 0;
    }
}
.menu label:hover {
    background: #ccc;
}
.menu li {
    float: left;
    @include mq(sp) {
        clear: left;
    }
}
.detailbox {
    border-radius: 20px;
    width: 100%;
    height: 418px;
    background-color: #EBEBEB;
    @include mq(sp) {
        background-color: #FFFFFF;
    }
}
.detail {
    display: flex;
    flex-flow: column;
    width: 20%;
    margin: 40px 0 auto 60px;
    @include mq(sp) {
        margin: 40px 0 0 0;
        width: 100%;
    }
    &__item {
        display: flex;
        flex-flow: row;
        align-items: flex-end;
        padding-bottom: 36px;
        @include mq(sp) {
            padding-bottom: 20px;
        }
    }
    &__img {
        height: 35px;
        margin-right: 24px;
    }
    &__text {
        font-family: Hiragino sans;
        font-size: 16px;
        font-weight: 400;
        letter-spacing: 0.28em;
        line-height: 2;
        text-align: left;
        white-space: pre-wrap;
    }
    &-note {
        display: flex;
        justify-content: flex-end;
        margin-bottom: 64px;
        text-align-last: left;
        font-family: Hiragino sans;
        font-size: 16px;
        font-weight: 400;
        letter-spacing: 0.28em;
        line-height: 1.5;
        white-space: pre-wrap;
        @include mq(sp) {
            width: 98%;
            background-color: #EBEBEB;
            margin: 50px 0 0 0;
            padding: 0.5em;
        }
    }
}

</style>