<template>
    <div class="indexPage" v-title data-title="首页">
        <div class="navTopBarHome">
            <rightBar></rightBar>
        </div>

        <div class="bannerArea">
            <!-- Swiper -->
            <swiper :options="swiperOption" ref="mySwiper"  v-if="bannerList.length>0">
                <div class="swiper-slide swiper-no-swiping" v-for="(itemBanner,index) in bannerList" :key = "(itemBanner,index)">
                    <div class="swiperLeft">
                        <div class="infoBanner">
                            <p class="introBanner"><span v-for="(item,index) in itemBanner.labs">{{item}}</span></p>
                            <h2 class="name">{{itemBanner.name}}</h2>
                            <h2 class="name">{{itemBanner.nameEnglish}}</h2>
                            <p class="lineArea"></p>
                            <p class="introDetail">{{itemBanner.intro}}</p>
                            <router-link :to="{path:'/productCenterDetail',query:{type_id:itemBanner.type_id,product_id:itemBanner.product_id}}"  tag="a" target="_blank" class="goProduct goMoreDetail"> 立即租赁产品  > </router-link>
                        </div>
                    </div>
                    <div class="swiperRight">
                        <!--<img :src="itemBanner.image" alt="" >-->
                        <div class="imgRightBanner" :style="{'background-image':'url('+itemBanner.image+')'}"></div>
                    </div>
                </div>
                <!-- Add Pagination -->
                <div class="swiper-button-prev swiper-button-prev-banner" slot="button-prev"></div>
                <div class="swiper-button-next swiper-button-next-banner" slot="button-next"></div>

                <!--<div class="swiper-pagination swiper-paginationBannernav"></div>-->
                <div class="swiper-pagination" slot="pagination"></div>
                <!--分页样式-->
                <!--<div class="swiper-pagination2" slot="pagination2"></div>-->

            </swiper>
        </div>


        <div class="FourIntroArea">
            <h2 class="title">“从探索到发现， </h2>
            <p class="intro">我们的目的就是为了让你收获惊喜”</p>
            <p class="goRule"><router-link to="/leaseRules"  tag="a" target="_blank" class="goMoreDetail"> 更多租赁规则  > </router-link></p>
            <div class="tabArea">
                <div class="tabName">
                    <div class="NameOne" @click="tabChange(index)"  v-for="(item,index) in tabArray" :key="index">
                        <img :src="item.image" alt="">
                        <p class="name">{{item.word}}</p>
                    </div>
                </div>
                <div class="tabContent">
                    <div class="contentOne" v-show="isTabActive === 0"><p>依托于蚂蚁金服完善的信用体系，用户绑定了支付宝芝麻信用，且650 分以上可享受押金减免服务，芝麻分数越高，免押额度越多，最高可实现押金全免，所有产品均适用。每一次用芝麻分下单，都让你的芝麻信用更有价值。</p></div>
                    <div class="contentOne contentTwo" v-show="isTabActive === 1"><p>无论是热门的游戏产品、酷炫的无人机、高画质的相机镜头、震撼的影音产品，还是新奇的酷玩数码，都能在这里找到。 探物致力于传播科技便捷生活，将前沿、实用的科技产品带到更多普通用户的手中，让用户无需占有，即可享受。</p></div>
                    <div class="contentOne contentThree" v-show="isTabActive === 2"><p>依托于蚂蚁金服完善的信用体系，用户绑定了支付宝芝麻信用，且650 分以上可享受押金减免服务，芝麻分数越高，免押额度越多，最高可实现押金全免，所有产品均适用。每一次用芝麻分下单，都让你的芝麻信用更有价值。</p></div>
                    <div class="contentOne contentFour"  v-show="isTabActive === 3"><p>您购买了「安心享」服务后，在产品的租赁期间，因人为造成的产品磨损、毁坏、进水，和快递运输寄回途中损坏的维修风险，由探物承担 70%，用户只需要承担 30% 的维修费用。 </p></div>
                </div>
            </div>
        </div>

        <div class="InformationZX">
            <div class="InformationMain">
                <div class="topArea">
                    <h2 class="title">资讯动态</h2>
                    <p class="intro">一起分享生活，一起收获惊喜</p>
                </div>
                <router-link to="/dynamic/userDynamics" class="understandMore">了解更多</router-link>
                <div class="scrollAreaZX">
                    <div class="scrollActionMain">
                        <div class="scrollItem">
                            <!-- Swiper -->
                            <swiper :options="swiperOptionZX" ref="mySwiper">
                                <div class="swiper-slide" v-for="(item,index) in productsListZX" :key = "(item,index)">
                                    <router-link :to="{path:'/dynamic/graphicInformationDetail',query:{themeId:item.themeId}}"  tag="a" target="_blank">
                                    <div class="InformationOne">
                                        <div class="imgZX"><img :src="item.themeBigImage" alt="" class="imgZX"> <span class="tagName">{{item.themeTag}}</span></div>
                                        <div class="userInfoTime">
                                            <img :src="item.sourceLogo" alt="" class="userLOGO">
                                            <span class="name">{{item.sourceName}}</span>
                                            <i class="circle">.</i>
                                            <span class="time">{{item.datetime | formatTime11}}</span>
                                        </div>
                                        <h2 class="title">{{item.themeTitle}}</h2>
                                        <p class="intro">{{item.themeDesc}}</p>
                                        <a href="#" class="readMore">READ MORE  ></a>
                                    </div>
                                    </router-link>
                                </div>
                                <!-- Add Pagination -->
                                <div class="swiper-button-prev" slot="button-prev"></div>
                                <div class="swiper-button-next" slot="button-next"></div>
                            </swiper>

                        </div>
                    </div>
                </div>
            </div>
        </div>

        <div class="aboutUsArea">
            <div class="aboutUsAreaMain">
                <div class="topArea">
                    <h2 class="title">关于我们</h2>
                    <p class="intro">新奇科技数码租赁平台</p>
                </div>
                <div class="usMain">
                    <div class="leftArea">
                        <div class="oneHistory">
                            <div class="left">
                                <div class="verticalLine">
                                    <p class="wordNum">01</p>
                                </div>
                                <h2 class="title">我们是谁？</h2>
                                <p class="introduction">探物（tanworth）成立于2016年3月，是国内首家引领新奇科技数码租赁模式的成长型企业，目前在深圳、北京、武汉、杭州、厦门有5个网点分布，用户通过探物App可以租借到心仪的各类数码产品。</p>
                            </div>
                        </div>
                        <div class="oneHistory">
                            <div class="left">
                                <div class="verticalLine">
                                    <p class="wordNum">02</p>
                                </div>
                                <h2 class="title">我们做什么？</h2>
                                <p class="introduction">探物（tanworth）为用户提供最新、最酷和最为实用的科技数码产品，用户通过探物选择心仪的科技产品进行付费租赁，并创作分享高质量、好玩的科技视频和图文资讯，用户也能在探物发表产品的使用口碑，交流体验心得。 </p>
                            </div>
                        </div>
                        <router-link to="/aboutUs" class="understandMoreUs">了解更多</router-link>
                    </div>
                </div>
            </div>
            <div class="rightArea">
                <a href="javascript:;" onclick="document.getElementById('video').play()" class="videoClick"  @click="maskVideo=!maskVideo"></a>
                <div class="maskVideo" v-show="maskVideo===true" @click="maskVideo=!maskVideo" onclick="document.getElementById('video').pause()"></div>
                <video :src="videoOne.index_video" id="video" controls="controls" class="videoOkPlay" v-show="maskVideo===true" >
                    当前浏览器不支持 video直接播放,请升级
                </video>
            </div>
        </div>

        <div class="ourPartner">
            <div class="ourPartnerMain">
                <div class="topArea">
                    <h2 class="title">合作伙伴</h2>
                    <p class="intro">前进的路上，我们一起成长收获感动</p>
                </div>
            </div>
            <div class="scrollLogoArea">
                <!-- Swiper -->
                <swiper :options="swiperOptionLOGO" ref="mySwiper">
                    <div class="swiper-slide">
                        <div class="logoPartner" >
                            <img src="static/img/1@2x.png" alt="">
                            <i class="rightLine"></i>
                            <i class="bottomLine"></i>
                        </div>
                        <div class="logoPartner" >
                            <img src="static/img/2@2x.png" alt="">
                            <i class="rightLine"></i>
                            <i class="bottomLine"></i>
                        </div>
                        <div class="logoPartner" >
                            <img src="static/img/3@2x.png" alt="">
                            <i class="rightLine"></i>
                            <i class="bottomLine"></i>
                        </div>
                        <div class="logoPartner" >
                            <img src="static/img/4@2x.png" alt="">
                            <i class="bottomLine"></i>
                        </div>
                        <div class="logoPartner" >
                            <img src="static/img/5@2x.png" alt="">
                            <i class="rightLine"></i>
                        </div>
                        <div class="logoPartner" >
                            <img src="static/img/6@2x.png" alt="">
                            <i class="rightLine"></i>
                        </div>
                        <div class="logoPartner" >
                            <img src="static/img/7@2x.png" alt="">
                            <i class="rightLine"></i>
                        </div>
                        <div class="logoPartner" >
                            <img src="static/img/8@2x.png" alt="">
                        </div>
                    </div>
                    <div class="swiper-slide">
                        <div class="logoPartner" >
                            <img src="static/img/8@2x.png" alt="">
                            <i class="rightLine"></i>
                            <i class="bottomLine"></i>
                        </div>
                        <div class="logoPartner" >
                            <img src="static/img/10@2x.png" alt="">
                            <i class="rightLine"></i>
                            <i class="bottomLine"></i>
                        </div>
                        <div class="logoPartner" >
                            <img src="static/img/11@2x.png" alt="">
                            <i class="rightLine"></i>
                            <i class="bottomLine"></i>
                        </div>
                        <div class="logoPartner" >
                            <img src="static/img/12@2x.png" alt="">
                            <i class="bottomLine"></i>
                        </div>
                        <div class="logoPartner" >
                            <img src="static/img/13@2x.png" alt="">
                            <i class="rightLine"></i>
                        </div>
                        <div class="logoPartner" >
                            <img src="static/img/14@2x.png" alt="">
                            <i class="rightLine"></i>
                        </div>
                        <div class="logoPartner" >
                            <img src="static/img/15@2x.png" alt="">
                            <i class="rightLine"></i>
                        </div>
                        <div class="logoPartner" >
                            <img src="static/img/16@2x.png" alt="">
                        </div>
                    </div>
                    <div class="swiper-slide">
                        <div class="logoPartner" >
                            <img src="static/img/17@2x.png" alt="">
                            <i class="rightLine"></i>
                            <i class="bottomLine"></i>
                        </div>
                        <div class="logoPartner" >
                            <img src="static/img/18@2x.png" alt="">
                            <i class="rightLine"></i>
                            <i class="bottomLine"></i>
                        </div>
                        <div class="logoPartner" >
                            <img src="static/img/19@2x.png" alt="">
                            <i class="rightLine"></i>
                            <i class="bottomLine"></i>
                        </div>
                        <div class="logoPartner" >
                            <img src="static/img/20@2x.png" alt="">
                            <i class="bottomLine"></i>
                        </div>
                        <div class="logoPartner" >
                            <img src="static/img/21@2x.png" alt="">
                            <i class="rightLine"></i>
                        </div>
                        <div class="logoPartner" >
                            <img src="static/img/22@2x.png" alt="">
                            <i class="rightLine"></i>
                        </div>
                        <div class="logoPartner" >
                            <img src="static/img/23@2x.png" alt="">
                            <i class="rightLine"></i>
                        </div>
                        <div class="logoPartner" >
                            <img src="static/img/24@2x.png" alt="">
                        </div>
                    </div>
                    <!-- Add Pagination -->
                    <div class="swiper-pagination" slot="pagination"></div>
                </swiper>

            </div>
        </div>

        <rightScrollTop></rightScrollTop>
        <footerBar></footerBar>
    </div>
</template>

<script>
    import { CONFIG } from  '../assets/js/config';
    import { network } from '../assets/js/network';
    import rightBar from './rightBar'
    import rightScrollTop from './rightScrollTop'
    import footerBar from './footerBar'
    import 'swiper/dist/css/swiper.css'
    import { swiper, swiperSlide } from 'vue-awesome-swiper'
    export default {
        name: 'indexPage',
        components: {
            rightBar,
            rightScrollTop,
            footerBar,
            swiper,
            swiperSlide
        },
        data () {
            return {
                isTabActive: 0,
                tabArray:[
                    {image:'static/img/homeTab1.png',word:'绑定芝麻分免押金'},
                    {image:'static/img/homeTab2.png',word:'海量产品任意选 '},
                    {image:'static/img/homeTab3.png',word:'绑定芝麻分免押金 '},
                    {image:'static/img/homeTab4.png',word:'产品安心享'}
                ],

                maskVideo:false,
                swiperOption:{//BANNER
                    notNextTick: true,
                    loop: true,//循环
                    autoplay: true, //自动轮播
                    spaceBetween: 30,
                    effect: 'fade',
                    onlyExternal:true,//禁止拖拽
                    navigation: {
                        nextEl: '.swiper-button-next-banner',
                        prevEl: '.swiper-button-prev-banner',
                    },

                    pagination: {
                        el: '.swiper-pagination',
                        clickable: true,
                    },
                   /* pagination: {
                        el: '.swiper-pagination2',
                        type: 'fraction',//设置像1/n分页类型
                    },*/
                    observer: true, //修改swiper自己或子元素时，自动初始化swiper
                    observeParents: true, //修改swiper的父元素时，自动初始化swiper
        },

                swiperOptionZX:{//资讯板块轮播
                    notNextTick: true,
                    slidesPerView: 3.18,
                    slidesPerGroup: 3,
                    loop: false,
                    loopFillGroupWithBlank: true,//最后一个后面的空白

                    navigation: {
                        nextEl: '.swiper-button-next',
                        prevEl: '.swiper-button-prev',
                    },
                    observer: true, //修改swiper自己或子元素时，自动初始化swiper
                    observeParents: true, //修改swiper的父元素时，自动初始化swiper
                },

                swiperOptionLOGO:{//合作伙伴
                    loop: true,//循环
                    notNextTick: true,
                    autoplay: true, //自动轮播
                    slidesPerView: 'auto',
                    pagination: {
                        el: '.swiper-pagination',
                        clickable: true,
                    },
                    observer: true, //修改swiper自己或子元素时，自动初始化swiper
                    observeParents: true, //修改swiper的父元素时，自动初始化swiper
                },
                bannerList:[],//banner图
                productsListZX:[],//资讯
                videoOne:{},//视频
            }
        },
        created(){
            var that = this;
            that.getData();//banner
        },
        mounted() {

        },
        methods:{
            getData(){//banner
                var that = this;
                network(CONFIG.banners,{},{method:'GET'}).then((res) => {
                    console.log(res)
                    that.bannerList=res.details.banners;//banner
                    that.videoOne=res.details.videos;//视频
                    that.productsListZX=res.details.themes;//资讯
                });
            },
            tabChange (index) {
                this.isTabActive = index
            },
        }
    }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

    .bannerArea{position: relative;background:#fff;width: 100%;height:1100px;}
    .bannerArea .swiperLeft{width: 44%; /*width: 860px;*/height: 960px;float: left;background:rgba(242,242,242,1);position: relative;position: absolute;top:0px;left: 0;z-index: -1;}
    .bannerArea .swiperLeft .infoBanner{width: 500px;margin-top: 200px;margin-left: 140px;}
    .bannerArea .swiperLeft .infoBanner .introBanner{margin-bottom: 17px;}
    .bannerArea .swiperLeft .infoBanner .introBanner span{font-size: 14px;color:rgba(51,51,51,1);margin-right: 24px;}
    .bannerArea .swiperLeft .infoBanner .name{font-size: 38px;color:rgba(34,34,34,1);line-height:54px;}
    .bannerArea .swiperLeft .infoBanner .lineArea{width:40px;height:12px;background:rgba(34,34,34,1);margin: 14px 0 28px;}
    .bannerArea .swiperLeft .infoBanner .introDetail{font-size: 18px;color:rgba(34,34,34,1);margin-bottom: 26px;line-height:35px;height: 140px;width: 440px;}
    .bannerArea .swiperLeft .infoBanner .goProduct{font-size: 14px;color:rgba(34,34,34,1);}

    .bannerArea /deep/ .swiper-button-prev{left: 140px;top: 75%;background-color: rgba(62,216,196,1);width: 60px;height: 60px;background-image:url("../../static/img/swiper-left.png");background-size: cover;}
    .bannerArea /deep/ .swiper-button-next{left: 214px;top: 75%;background-color: rgba(62,216,196,1);width: 60px;height: 60px;background-image:url("../../static/img/swiper-right.png");background-size: cover;}
    /*.bannerArea /deep/ .swiper-pagination-fraction{color: #fff;width: 18px;right: 40px;}*/

    .bannerArea /deep/ .swiper-pagination.swiper-pagination-clickable.swiper-pagination-bullets{position: absolute; left: 98%;top: 40%; width: 4px;}
    .bannerArea /deep/ .swiper-pagination-bullet{width: 4px;height: 4px;background:#fff;opacity: 1;}
    .bannerArea /deep/ .swiper-pagination-bullet.swiper-pagination-bullet-active{height: 40px;background: #fff;border-radius: 0;margin-top: 10px;}

    .bannerArea .swiperRight{width: 64%; /*width: 1240px;*/height: 900px;float: right;margin-top: 120px;}
    /*.bannerArea .swiperRight img{width: 1240px;height: 900px;}*/
    .bannerArea .swiperRight .imgRightBanner{width:100%;height: 100%;background-size: cover;background-position: center;}

    /*go多变色线条动画 */
    .goMoreDetail{display: inline-block;height: 26px;line-height: 26px;border-bottom: 2px solid rgba(170,170,170,1); font-size: 14px;color:rgba(170,170,170,1);position: relative;}
    .goMoreDetail:before {position: absolute;content: '';border-top: 3px solid #000;z-index: 1;width: 0;top: 30px;left: 0;}
    .goMoreDetail:after {position: absolute;width: 0%;content: '';border-top: 2px solid #3ED8C4;top: 26px;left: 0;}
    .goMoreDetail:hover{color:rgba(62,216,196,1);}
    .goMoreDetail:hover:after {width: 100%;
        transition:width 0.4s;
        -moz-transition:width 0.4s; /* Firefox 4 */
        -webkit-transition:width 0.4s; /* Safari and Chrome */
        -o-transition:width 0.4s; /* Opera */
        transition-timing-function: linear;
    }


    /*从探索到发现*/
    .FourIntroArea{padding: 0px 0 100px;}
    .FourIntroArea .title{font-size: 34px;color:rgba(34,34,34,1);text-align:center;}
    .FourIntroArea .intro{font-size: 24px;color:rgba(34,34,34,1);text-align:center;margin: 16px 0 20px;}
    .FourIntroArea .goRule{font-size: 14px;color: rgba(34,34,34,1);text-align: left;width: 115px;margin: 0 auto 50px;display: block;}

    .FourIntroArea .tabArea{width: 1100px;height: 380px;margin: 0 auto;-webkit-box-shadow: 0 0 10px #dedede;box-shadow: 0 0 10px #dedede;}
    .FourIntroArea .tabArea .tabName{width: 1100px;height: 200px;position: relative;margin-left: 115px;}
    .FourIntroArea .tabArea .tabName .NameOne{width: 130px;float: left;margin-right: 120px;cursor: pointer;margin-top: 35px;}
    .FourIntroArea .tabArea .tabName .NameOne img{display: block; width: 120px;height: 120px;margin: 0 auto;}
    .FourIntroArea .tabArea .tabName .NameOne .name{text-align: center;font-size: 16px;font-weight: 600;color:rgba(62,216,196,1);}
    .FourIntroArea .tabContent{width: 940px;height: 113px;margin:0 auto;}
    .FourIntroArea .tabContent .contentOne{width: 940px;height: 113px;background: url("../../static/img/kuang.png");background-size: cover;}
    .FourIntroArea .tabContent .contentOne p{padding: 40px 50px;line-height:24px;}
    .FourIntroArea .tabContent .contentTwo{width: 940px;height: 113px;background: url("../../static/img/kuang2.png");background-size: cover;}
    .FourIntroArea .tabContent .contentThree{width: 940px;height: 113px;background: url("../../static/img/kuang3.png");background-size: cover;}
    .FourIntroArea .tabContent .contentFour{width: 940px;height: 113px;background: url("../../static/img/kuang4.png");background-size: cover;}








    /*资讯板块*/
    .InformationZX{height: 1000px;background:rgba(242,242,242,1);position: relative;}
    .InformationZX .InformationMain{width: 1000px;margin:0 auto ;padding-top: 136px}
    .InformationZX .topArea{position: relative;margin-bottom: 50px;}
    .InformationZX .topArea .title{font-size: 34px;color:rgba(34,34,34,1);line-height: 36px;}
    .InformationZX .topArea .intro{font-size: 16px;color:rgba(102,102,102,1);line-height: 36px;margin-top: 10px;}
    .InformationZX .understandMore{display: block; width: 140px;height: 40px;line-height: 40px;border: 1px solid rgba(34,34,34,1);color:rgba(34,34,34,1);text-align: center;position: absolute;right: 270px;top: 151px;}

    .scrollAreaZX{width: 1500px;height: 780px;overflow: hidden; background-color: #fff;}
    .scrollAreaZX{}
    .scrollAreaZX /deep/ .swiper-container{overflow-y: visible;margin-right: 50px;}
    .scrollAreaZX /deep/ .swiper-button-prev{top:105px; left: 0px;background-color: rgba(62,216,196,1);width: 60px;height: 60px;background-image:url("../../static/img/swiper-left.png");background-size: cover; }
    .scrollAreaZX /deep/ .swiper-button-next{top:105px; right: 0; background-color: rgba(62,216,196,1);width: 60px;height: 60px;background-image:url("../../static/img/swiper-right.png");background-size: cover;}
    @media screen and (max-width: 1366px) {
        .scrollAreaZX /deep/ .swiper-button-next{right: 115px;}
    }
    @media screen and (max-width: 1280px) {
        .scrollAreaZX /deep/ .swiper-button-next{right: 125px;}
    }

    .scrollAreaZX /deep/ .swiper-button-prev.swiper-button-disabled,.scrollAreaZX /deep/ .swiper-button-next.swiper-button-disabled{opacity: 0;}

    .scrollActionMain{padding: 133px 0 0 93px;}
    .InformationOne{width: 375px;height: 540px;float: left;margin:0 58px 0 0;position: relative;}
    .InformationOne .imgZX{width: 375px;height: 230px;background-color: #f7f7f7;}
    .InformationOne .imgZX .tagName{position: absolute;top:10px;left: 10px;font-size: 12px;color: #fff;padding: 2px 16px;background-color: #3ED8C4;}
    .InformationOne .userInfoTime{font-size: 14px;color:rgba(136,136,136,1);height: 22px;line-height: 22px;margin: 36px 0 18px;}
    .InformationOne .userInfoTime .userLOGO{width: 22px;height: 22px;border-radius: 50%;vertical-align: middle;}
    .InformationOne .userInfoTime .name{}
    .InformationOne .userInfoTime .time{}
    .InformationOne .title{font-size: 18px;color: rgba(34,34,34,1);line-height: 22px;height: 22px;overflow: hidden;text-overflow: ellipsis;white-space: nowrap;}
    .InformationOne .intro{font-size: 14px;color:rgba(102,102,102,1);line-height: 20px;height: 40px;margin: 22px 0 50px;
        overflow : hidden;
        text-overflow: ellipsis;
        display: -webkit-box;
        -webkit-line-clamp: 2;
        -webkit-box-orient: vertical;
    }


    /*关于我们*/
    .aboutUsArea{height: 810px;background:rgba(72,197,181,1);position: relative;}
    .aboutUsAreaMain {width: 1000px;margin:0 auto ;padding-top: 96px;}
    .aboutUsAreaMain .topArea{position: relative;margin-bottom: 20px;}
    .aboutUsAreaMain .topArea .title{font-size: 34px;color:#fff;line-height: 36px;}
    .aboutUsAreaMain .topArea .intro{font-size: 16px;color:#fff;line-height: 36px;margin-top: 10px;}
    .usMain{position: relative;height: 620px;}
    .usMain .leftArea{width: 400px;float: left;}
    .usMain .leftArea .oneHistory{position: relative;width: 345px;height: auto;overflow: hidden;float: left;margin-right: 50px;}
    .usMain .leftArea .oneHistory.margR{margin-right: 0;}
    .usMain .leftArea .oneHistory .left{padding-left: 57px;padding-top: 40px;position: relative;}
    .usMain .leftArea .oneHistory .left .verticalLine{width:2px;height:100px;background:#fff;position: absolute;top:45px;left: 0;}
    .usMain .leftArea .oneHistory .left .verticalLine .wordNum{font-size:16px;color:#fff;padding-left: 8px;}
    .usMain .leftArea .oneHistory .left .title{font-size: 20px;color: #fff;margin-bottom: 18px;font-weight: 600;}
    .usMain .leftArea .oneHistory .left .introduction{font-size: 14px;color: #fff;line-height:26px;}
    .usMain .leftArea .understandMoreUs{display: block; width: 140px;height: 40px;line-height: 40px;border: 1px solid #fff;color:#fff;text-align: center;position: absolute;left: 58px;bottom: 116px;}
    .aboutUsArea .rightArea{width: 52%; /*width: 960px;*/height: 690px;position: absolute;right: 0;top: 240px;background: url("https://resource.tanwuapp.com/Fo0RzXUbXA6Hbk364VtcBqPziUkn"); /*background: url("../../static/img/indexaboutus.png");*/background-size: cover;background-position: left;}
    .aboutUsArea .rightArea .videoClick{width: 300px;height: 100px;position: absolute;left: 0;bottom: 0;}
    .aboutUsArea .rightArea  .maskVideo{ width: 100%;height: 100%;position: fixed;left: 0;top: 0;right: 0;bottom: 0;background: rgba(0,0,0,.8);z-index:105;}
    .aboutUsArea .rightArea .videoOkPlay{width:1000px;height: 600px;position: fixed;left: 50%;top:50%;transform: translate(-50%, -50%);z-index: 106;}
    /*@media only screen and (max-width: 1366px) {*/
    /*.aboutUsArea .rightArea{width: 672px;height: 483px;}*/
    /*}*/
    /*合作伙伴*/
    .ourPartner{height: 738px;}
    .ourPartnerMain{width: 1000px;margin:0 auto ;padding-top: 136px;}
    .ourPartnerMain .topArea{position: relative;margin-bottom: 50px;}
    .ourPartnerMain .topArea .title{font-size: 34px;color:rgba(34,34,34,1);line-height: 36px;}
    .ourPartnerMain .topArea .intro{font-size: 16px;color:rgba(102,102,102,1);line-height: 36px;margin-top: 10px;}
    /*logo轮播*/
    .scrollLogoArea{position: relative;width: 1000px;height: auto;overflow: hidden;margin: 100px auto;}
    .scrollLogoArea .logoPartner{width: 190px;height: 80px;float: left;padding: 18px;position: relative;}
    .scrollLogoArea .logoPartner .rightLine{width:2px;height: 90px;position: absolute;right: 0;top:12px;background:rgba(238,238,238,1);}
    .scrollLogoArea .logoPartner .bottomLine{width: 200px;height: 2px;position: absolute;left: 11px;bottom: 0;background:rgba(238,238,238,1);}
    .scrollLogoArea /deep/ .swiper-pagination.swiper-pagination-clickable.swiper-pagination-bullets{position: absolute; left: 940px;top:102px; width: 60px;height:30px;}
    .scrollLogoArea /deep/ .swiper-pagination-bullet{width: 8px;height: 8px;}
    .scrollLogoArea /deep/ .swiper-pagination-bullet.swiper-pagination-bullet-active{background:rgba(62,216,196,1);}

    /*鼠标移入hover左右滚动按钮变色*/
    /deep/ .swiper-button-prev:hover,
    /deep/ .swiper-button-next:hover
    {background-color: #38cdba;}
</style>
