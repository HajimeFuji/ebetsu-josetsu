<template>
    <div class="page-wrap">
        <div class="topbox">
            <div class="ebeyuki">
                <router-link to="/">
                    <img src="../assets/ebeyuki_b.png" alt="" class="ebeyuki__img">
                    <img src="../assets/ebeyuki_sp_b.png" alt="" class="ebeyuki__img__sp">
                </router-link>
            </div>
            <div class="app-name">
                <p class="app-name__text">江別除雪ポータルアプリ</p>
            </div>
            <div class="infobox">
                <a href="https://lin.ee/SI9lzW0" class="" target="_blank" rel="noopener noreferrer">
                    <div class="btn">
                        <div class="btn__box">
                            <img src="../assets/top_LINE_2.png" alt="" class="btn__logo">
                            <p class="btn__text">除雪の予定を通知</p>
                        </div>
                        <!-- <div class="copyright__sp">
                            <p class="copyright__text">Copyright © 2022 えべ雪 -EbeYuki All Rights Reserved.</p>
                        </div> -->
                    </div>
                </a>
            </div>
        </div>
        <div class="infobox-sp">
            <a href="https://lin.ee/SI9lzW0" class="" target="_blank" rel="noopener noreferrer">
                <div class="btn">
                    <div class="btn__box">
                        <img src="../assets/top_LINE_2.png" alt="" class="btn__logo">
                        <p class="btn__text">除雪の予定を通知</p>
                    </div>
                    <div class="copyright__sp">
                        <p class="copyright__text">Copyright © 2022 えべ雪 All Rights Reserved.</p>
                    </div>
                </div>
            </a>
        </div>
        <div class="content">
            <div class="searchbox">
                <BtnVendor 
                    title="全排雪業者一覧" 
                    iconPath="bull.png" 
                    v-bind:vendorCount=vendors.length
                    v-bind:onClick=filterAll
                />
                <BtnVendor 
                    title="排雪" 
                    iconPath="dump.png" 
                    v-bind:vendorCount=removeSnowVendors.length
                    v-bind:onClick=filterRemoveSnow
                />
                <BtnVendor 
                    title="公道除雪後の間口の除雪・置雪除雪" 
                    iconPath="house.png" 
                    v-bind:vendorCount=misplaceVendors.length
                    v-bind:onClick=filterMisplace
                />
                <BtnVendor 
                    title="屋根の雪下ろし" 
                    iconPath="roof.png" 
                    v-bind:vendorCount=roofVendors.length 
                    isMini="true"
                    v-bind:onClick=filterRoof
                />
                <BtnVendor 
                    title="玄関通路の除雪" 
                    iconPath="door.png" 
                    v-bind:vendorCount=aisleVendors.length 
                    isMini="true"
                    v-bind:onClick=filterAisle
                />
            </div>
            
            <div class="returnbox">
                <a class="btn2__text" href="#">
                    <div class="btn2">
                        <p class="btn2__text">page top</p>
                        <img src="../assets/arrow-up.png" alt="" class="btn2__logo">
                    </div>
                </a>
            </div>

        </div>
        <div class="resultfield">
            <div id="result" class="resultdetail">
                <div class="searchForm">
                    <input type="search" class="text" placeholder="キーワードで絞る" v-bind:onChange="changeFilteringWord">
                    <button type="button" value="検索" v-bind:onClick="filtering">
                        <img src="../assets/arrow-dropright-circle.png" alt="">
                    </button>
                </div>
            </div>
            <div class="resultdetail resultdetail__bottom">
                <div  v-for="vendor in filterVendors" :key="vendor.id">
                    <VendorListItem v-bind:vendor='vendor' />
                </div>
            </div>
            <div class="line"></div>
            <div class="copyright">
                <p class="copyright__text">Copyright © 2022 えべ雪 All Rights Reserved.</p>
            </div>
        </div>
    </div>
</template>

<script>
import BtnVendor from '../components/BtnVendor.vue'
import VendorListItem from '../components/VendorListItem.vue'

export default {
    name: 'SearchView',
    components: {
        BtnVendor,
        VendorListItem
    },
    methods: {
        async getVendorInfo() {
            const response = await fetch('https://api.ebetsu-data.com/josetsu/gyosha', {
                headers: {
                    cache: 'no-store',
                    'Content-Type': 'application/json'
                },
            });

            this.vendors = await response.json()
            this.filterVendors = this.vendors

            this.aisleVendors = this.vendors.filter(item => item.aisle_snow_remove_flg === '1')
            this.misplaceVendors = this.vendors.filter(item => item.misplaced_snow_flg === '1')
            this.roofVendors = this.vendors.filter(item => item.roof_snow_remove_flg === '1')
            this.removeSnowVendors = this.vendors.filter(item => item.remove_snow_flg === '1')
        },
        filterAll() {
            this.filterVendors = this.vendors
            this.scrollToResilt()
        },
        filterAisle() {
            this.filterVendors = this.aisleVendors
            this.scrollToResilt()
        },
        filterMisplace() {
            this.filterVendors = this.misplaceVendors
            this.scrollToResilt()
        },
        filterRoof() {
            this.filterVendors = this.roofVendors
            this.scrollToResilt()
        },
        filterRemoveSnow() {
            this.filterVendors = this.removeSnowVendors
            this.scrollToResilt()
        },
        changeFilteringWord(e) {
            this.filteringWord = e.target.value
            location.href = '#result'
        },
        scrollToResilt() {
            document.getElementById('result').scrollIntoView({
                    behavior: 'smooth',
                    block: 'start'
                });            
        },
        filtering() {
            this.filterVendors = this.vendors.filter(
                item => {
                    const word = item.company_name
                                + item.company_name_kana 
                                + item.overview 
                                + item.zip_code 
                                + item.address 
                                + item.phone_number 
                                + item.aisle_snow_remove 
                                + item.misplaced_snow 
                                + item.roof_snow_remove 
                                + item.remove_snow

                    return word.indexOf(this.filteringWord) > -1
                }
            )
        }
    },
    beforeRouteEnter(_to, _from, next) {
        scroll({ top: 0 })
        next();
    },
    data() {
        return {
            vendors: [],
            aisleVendors: [],
            misplaceVendors: [],
            roofVendors: [],
            removeSnowVendors: [],
            filterVendors: [],
            filteringWord: ''
        }
    },
    mounted() {
        this.getVendorInfo()
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

a {
    text-decoration: none;
}
.page-wrap {
    display: flex;
    flex-flow: column;
    @include mq(sp){
        display: initial;
    }
}
.topbox {
    display: flex;
    width: 100%;
    height: 130px;
    @include mq(sp){
        display: flex;
        flex-wrap: wrap;
        justify-content: space-between;
        align-items: flex-end;
        width: 90%;
        height: 80px;
        margin: 0 auto;
    }
}
.ebeyuki {
    margin: auto 75px 0px 95px;
    width: 10%;
    @include mq(sp) {
        display: flex;
        width: 33%;
        margin: initial;
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
                align-items: flex-end;
                width: 100%;
                // margin-bottom: 8px;
            }
        }
    }
}
.app-name {
    display: flex;
    align-items: flex-end;
    @include mq(sp) {
        margin: auto 0 0 auto;
    }
    &__text {
        margin-bottom: 8px;
        font-family: Hiragino sans; 
        font-size: 24px;
        font-weight: 300;
        color: #000000;
        letter-spacing: 0.42em;
        @include mq(sp) {
            margin-bottom: 0;
            font-size: 16px;
            font-weight: 500;
            letter-spacing: 0.3em;
        }
    }
}
.infobox {
    display: flex;
    margin: 0 0 auto auto;
    @include mq(sp){
        display: none;
    }
}
.infobox-sp {
    display: none;
    @include mq(sp){
        display: block;
        width: 100%;
        position: fixed;
        bottom: 0px;
        left: 0px;
    }
}
.btn {
    display: flex;
    align-items: center;
    justify-content: center;
    width: 390px;
    aspect-ratio: 3;
    background-color: #024AEF;
    color: #FCFCFC;
    @include mq(sp){
        display: flex;
        flex-flow: column;
        width: 100%;
        height: 103px;
    }
    &__box {
        display: flex;
        flex-flow: row;
        align-items: center;
        @include mq(sp) {
            width: 100%;
            justify-content: center;
            align-items: center;
            margin-bottom: 12.5px;
        }
    }
    &__logo {
        width: 40px;
        height: 40px;
        margin-right: 27px;
        @include mq(sp){
            width: 50px;
            height: 50px;
            margin-right: 30px;
        }
    }
    &__text {
        font-family: Hiragino sans;
        font-size: 23px;
        font-weight: 400;
        letter-spacing: 0.47em;
        // @include mq(sp) {
        //     letter-spacing: 0.15em;
        // }
    }
}
.content {
    background: url(../assets/search_main.png) center center no-repeat;
    background-size: cover;
    width: 100%;
    aspect-ratio: 2.10;
    display: flex;
    flex-flow: column;
    align-items: center;
    justify-content: center;
}

.searchbox {
    display: flex;
    flex-wrap: wrap;
    justify-content: center;
    column-gap: 24px;
    row-gap: 24px;
    // width: 100vw;
    max-width: 1350px;
    @include mq(sp) {
        max-width: initial;
        width: 100%;
        margin-top: 78px;
        margin-bottom: 85px;
        column-gap: 22px;
        row-gap: 22px;
    }
}
.returnbox {
    position: fixed;
    bottom: 40px;
    right: 110px;
    @include mq(sp) {
        position: fixed;
        bottom: 120px;
        right: 6%;
    }
}
.btn2 {
    display: flex;
    flex-flow: column;
    align-items: center;
    justify-content: center;
    width: 122px;
    height: 74px;
    background-color: #024AEF;
    color: #FCFCFC;
    border-radius: 20px;
    @include mq(sp){

    }
    &__text {
        font-family: Hiragino sans;
        font-size: 20px;
        font-weight: 500;
        color: #FFFFFF;
        margin-bottom: 10px;
    }
    &__logo {
        width: 24px;
        height: 13.5px;
    }
}
.resultfield {
    display: flex;
    flex-flow: column;
    align-items: center;
    justify-content: center;
    width: 100%;
    background-color: #FFFFFF;
    @include mq(sp){
        display: block;
        // margin-top: 56px;
    }
}
.resultdetail {
    display: flex;
    flex-flow: column;
    width: 95%;
    background-color: white;
    @include mq(sp){
        display: block;
        width: 85%;
        margin: 0 auto;
    }
    &__bottom {
        @include mq(sp){
            padding-bottom: 240px;
        }
    }
}

.searchForm {
    margin: 125px auto 76px 0;
    border: 2px solid #000;
    height: 51px;
    width: 405px;
    display: flex;
    justify-content: center;
    @include mq(sp){
        margin: 55px auto;
        padding: initial;
        display: flex;
        width: 100%;
    }
    & input[type="search"]:focus-visible {
        border: none;
        outline: none;
    }
    & input[type="search"] {
        border: none;
        height: 50px;
        width: 95%;
        padding: 0 10px;
        border-right: none;
        font-family: Hiragino sans;
        font-size: 18px;
        @include mq(sp) {
            font-family: Hiragino sans;
            font-size: 18px;
        }
    }
    & button[type="button"] {
        border: none;
        background-color: #FFFFFF;
        padding: 0;
        width: 50px;
        height: 50px;
        text-align: center;
        cursor: pointer;
        & img {
            width: 33px;
            @include mq(sp) {
                width: 30px;
            }
        }
    }
}

.line {
    background-color: #C1C1C1;
    height: 1px;
    width: 88%;
    margin: 0 auto 17.5px;
    @include mq(sp){
        display: none;
    }
}

.copyright {
    display: flex;
    justify-content: end;
    width: 100%;
    height: 18px;
    margin-bottom: 25px;
    @include mq(sp) {
        display: none;
    }
    &__sp {
        display: none;
        @include mq(sp) {
            display: flex;
        }
    }
    &__text {
        font-size: 18px;
        font-family: Noto sans;
        color: #959595;
        font-weight: 300;
        letter-spacing: 0.1em;
        padding-right: 150px;
        @include mq(sp){
            font-size: 12px;
            color: #FFF5F5;
            font-weight: bold;
            padding: initial;
        }
    }
}

</style>
