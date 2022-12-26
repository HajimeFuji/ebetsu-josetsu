<template>
    <div class="page-wrap">
        <div class="content">
            <div class="topbox">
                <div class="ebeyuki">
                    <router-link to="/">
                        <img src="../assets/ebeyuki.png" alt="" class="ebeyuki__img">
                        <img src="../assets/ebeyuki_sp.png" alt="" class="ebeyuki__img__sp">
                    </router-link>
                </div>
                <NewInfo />
            </div>
            <div class="fukidashibox">
                <div class="fukidashi fukidashi">
                    <img src="../assets/top_fukidashi_1.png" alt="" class="fukidashi__img">
                    <p class="fukidashi__text" >LINEで市の除雪の予定を通知!</p>
                </div>
                <div class="fukidashi fukidashi">
                    <img src="../assets/top_fukidashi_2.png" alt="" class="fukidashi__img"> 
                    <p class="fukidashi__text" >間口の除雪や屋根の雪下ろし業者検索！</p>                   
                </div>
            </div>
            <div class="infobox">
                <a href="https://lin.ee/SI9lzW0" class="btn__regist" target="_blank" rel="noopener noreferrer">
                    <div class="btn btn__left">
                        <img src="../assets/top_LINE.png" alt="" class="btn__logo">
                        <p class="btn__text" >市のLINEに登録</p>
                    </div>
                </a>
                <router-link to="/search" class="btn__search">
                    <div class="btn btn__right">
                        <img src="../assets/top_snowflake.png" alt="" class="btn__logo">
                        <span>除雪業者検索</span>
                    </div>
                </router-link>
            </div>
            <div class="app-name">
                <p class="app-name__text">江別除雪ポータルアプリ</p>
            </div>
            <div class="sp">
                <p class="sp__text">LINE<small>で市の</small>除雪の予定<small>を通知!間口の除雪や屋根の雪下ろし</small>業者検索！</p>
            </div>
            <div class="copyright">
                <p class="copyright__text">Copyright © 2022 えべ雪 All Rights Reserved.</p>
            </div>
        </div>
    </div>
</template>

<script>
// import { mapActions } from "vuex"
import NewInfo from '../components/NewInfo.vue'

export default {
    name: 'HomeView',
    beforeRouteEnter(_to, _from, next) {
        scroll({top:0})
        next();
    },
    components: {
        NewInfo
    }    
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
.page-wrap {
    display: flex;
    height: 100%;
    @include mq(sp){
        display: initial;
    }
}
.content {
    background: url(../assets/front_snowman.png) center center no-repeat;
    background-size: cover;
    opacity: 0.85;
    width: 100%;
    height: 100%;
    display: flex;
    flex-flow: column;
    // justify-content: center;
    @include mq(sp){
        background: url(../assets/front_snowman_sp.png) center center no-repeat;
        width: 100%;
        // height: 100%;
        // aspect-ratio: 0.64;
        justify-content: space-between;
    }
}
.topbox {
    display: flex;
    justify-content: space-between;
    align-items: flex-start;
    margin-top: 53px;
    @include mq(sp){
        display: block;
        margin: 0 7%;
    }
}
.ebeyuki {
    margin-left: 105px;
    width: 11.6%;
    // aspect-ratio: 0.42;
    @include mq(sp) {
        display: flex;
        width: 33%;
        margin: initial;
        position: absolute;
        top: 15px;
        left: 6%;
    }
    &__img {
        width: 100%;
        @include mq(sp) {
            display: none;
        }
        &__sp {
            display: none;
            @include mq(sp){
                display: flex;
                width: 100%;
            }
        }
    }
}
.app-name {
    display: flex;
    justify-content: center;
    font-family: Hiragino sans; 
    font-size: 28px;
    font-weight: 400;
    color: white;
    letter-spacing: 0.42em;
    text-shadow: 2px 2px 2px #000;
    @include mq(sp) {
        margin: inherit;
        display: flex;
        position: absolute;
        top: 50px;
        right: 5%;
    }
    &__text {
        padding: 16px;
        @include mq(sp) {
            font-size: 0.57em;
            width: 100%;
            letter-spacing: 0.15em;
            // justify-content: stretch;
            text-shadow: none;
        }
    }

}
.sp {
    display: none;
    width: 100%;
    @include mq(sp) {
        display: block;
    }
    &__text {
        @include mq(sp) {
            width: 85%;
            height: 54px;
            font-family: Noto Sans CJK JP;
            font-size: 20px;
            font-weight: bold;
            color: #000000;
            letter-spacing: 0.38em;
            text-align: justify;
            text-shadow: 2px 2px 1px #FFFFFF;
            text-align: left;
            margin: 20px auto;
        }
    }
}
.copyright {
    display: flex;
    justify-content: end;
    width: 100%;
    margin-bottom: 25px;
    @include mq(sp){
        display: block;
        justify-content: center;
        width: 100%;
        margin-bottom: 17px;
    }
    &__text {
        font-size: 18px;
        font-family: Noto sans;
        color: white;
        font-weight: bold;
        padding-right: 120px;
        @include mq(sp){
            display: flex;
            align-items: flex-end;
            justify-content: center;
            padding: initial;
            font-size: 12px;
            width: 100%;
            height: 20px;
        }
    }
}
.fukidashibox {
    width: 100%;
    display: flex;
    justify-content: center;
    margin: auto 0 0;
    @include mq(sp){
        display: none;
    }
}
.fukidashi {
    width: 100%;
    height: 320px;
    // margin-top: 340px;
    position: relative;
    justify-content: space-between;
    &__img {
        width: 320px;
        height: 320px;
    }
    &__text {
        position: absolute;
        top: 45%;
        left: 50%;
        transform: translate(-50%, -50%);
        font-family: Hiragino sans;
        font-size: 26px;
        letter-spacing: 0.38em;
        width: 200px;
    }
}
.infobox {
    display: flex;
    justify-content: center;
    @include mq(sp){
        display: block;
        width: 100%;
    }
}
.btn {
    display: flex;
    align-items: center;
    justify-content: center;
    // width: 390px;
    width: calc(100vw * 0.3);
    height: 87px;
    border: 5px solid #024AEF;
    box-shadow: 3px 3px 3px #FFFFFF;

    @include mq(tab) {
        width: calc(100vw * 0.45);
    }

    @include mq(sp){
        display: block;
        width: 85%;
        height: 74px;
        box-shadow: 5px 5px 3px rgba($color: #000000, $alpha: 0.25);
        margin: 0 auto;
    }
    &__left {
        display: flex;
        background-color: #FFFFFF;
        color: #0007B7;
        border-radius: 20px 0 0 20px;
        @include mq(sp){
            border-radius: 10px;
            margin-top: 32px;
        }
    }
    &__right {
        display: flex;
        background-color: #024AEF;
        color: #FCFCFC;
        border-radius: 0 20px 20px 0;
        cursor: pointer;
        @include mq(sp){
            border-radius: 10px;
            margin-top: 22px;
        }
    }
    &__logo {
        width: 40px;
        height: 40px;
        margin-right: 30.5px;
        @include mq(sp){
            width: 50px;
            height: 50px;
            margin-right: 30px;
        }
    }
    &__text {
        font-family: Hiragino sans;
        font-size: 28px;
        color: #0007B7;
        letter-spacing: 0.21em;
        @include mq(sp) {
            letter-spacing: 0.12em;
        }
    }
    &__regist {
        text-decoration: none;
    }
    &__search {
        font-family: Hiragino sans;
        font-size: 28px;
        letter-spacing: 0.38em;
        color: #FCFCFC;
        text-decoration: none;
    }
}

</style>
