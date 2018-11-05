<template>
    <div class="rightBar">
        <div class="navArea" id="navBar" :class="isFixed == true ? 'Fixed' :''">
            <router-link to="/"><img src="static/img/logo.png" alt="" class="logo"></router-link>
            <ul class="navFloatRight">
                <li><router-link to="/indexPage" class="goPage"><span class="bgNavItem">首页</span><span class="btmLine"></span></router-link></li>
                <li><router-link to="/aboutUs" class="goPage"><span class="bgNavItem">关于我们</span><span class="btmLine"></span></router-link></li>
                <li><router-link to="/product" class="goPage"><span class="bgNavItem">产品中心</span><span class="btmLine"></span></router-link></li>
                <li class="userDynamicsNav">
                    <router-link to="/dynamic" class="goPage"><span class="bgNavItem">资讯动态</span><span class="btmLine"></span></router-link>
                    <div class="childGoPage">
                        <router-link to="/dynamic/userDynamics" class="childPage"><span class="bgNavItemTwo">用户动态</span></router-link>
                        <router-link to="/dynamic/graphicInformation" class="childPage"><span class="lineTop"></span><span class="bgNavItemTwo">图文资讯 </span><span class="linebtm"></span></router-link>
                        <router-link to="/dynamic/tanwuVideo" class="childPage"><span class="bgNavItemTwo">探物视频</span></router-link>
                    </div>
                </li>
                <li><router-link to="/contactUs" class="goPage"><span class="bgNavItem">联系我们</span><span class="btmLine"></span></router-link></li>
                <li>
                    <div class="showLoginWord" v-show="noLogin" @click="loginComponentsShow" >登录/注册</div>
                    <div class="showLoginIcon" v-show="Login"  @click="userEditFlag = true">
                        <!--登陆已经编辑过图像-->
                        <div :style="{'background-image':'url('+selfInfo.headImg+')'}"  class="alreadyLogin" v-if="selfInfo.uuid"></div>
                        <!--登陆还未上传头像使用默认头像-->
                        <img src="static/img/login2.png" alt="" class="alreadyLogin" v-else>
                    </div>
                </li>
            </ul>
        </div>

        <!--登录注册区域-->
        <Login v-show="LoginShow"  @close="closeLogin"></Login>
        <userEditer v-if = "userEditFlag" @close="closeUserEditer"></userEditer>
    </div>
</template>

<script>


    import Login from './Login'
    import userEditer from './userEditer'
    import { CONFIG } from  '../assets/js/config';
    import { network } from '../assets/js/network';

    export default {
        name: 'rightBar',
        components:{
            Login,
            userEditer
        },
        data () {
            return {
                isFixed:false,
                isActive: false,
                loginComponentsArea:false,
                LoginShow: false,//登录框默认false
                userEditFlag:false,

                noLogin:true,//右上角没有登陆状态的icon
                Login:false,//右上角登陆状态
                selfInfo: "",

            }
        },
        created(){
            //登陆和未登录默认头像切换
            if(localStorage.getItem("twUser")) {
                this.noLogin=false;
                this.Login=true;
            }else{
                this.noLogin=true;
                this.Login=false;
            }
        },
        mounted(){
            var that = this;
            if(localStorage.getItem("selfInfo")) {
                this.selfInfo = JSON.parse(localStorage.getItem("selfInfo"));
            }
            //获取登陆后用户头像信息
            network(CONFIG.user, {}, {
                codeFlag: true
            }).then((res) => {
                if(res.head.code == 0) {
                    this.selfInfo = res.details;
                    localStorage.setItem("selfInfo", JSON.stringify(that.selfInfo))
                }
            });
            window.addEventListener('scroll', this.handleScroll)
        },
        destroyed () {
            window.removeEventListener('scroll', this.handleScroll)
        },
        methods:{
            handleScroll () {
                var scrollTop = window.pageYOffset || document.documentElement.scrollTop || document.body.scrollTop;
                var offsetTop = document.querySelector('#navBar').offsetTop;
                if (scrollTop>offsetTop) {
                    this.isFixed = true
                } else {
                    this.isFixed = false
                }
            },

            loginComponentsShow(){//点右上角登录框显示
                this.LoginShow = true;
            },
            closeLogin(){//关闭登录
                this.LoginShow = false;
            },
            closeUserEditer(){//关闭编辑
                this.userEditFlag = false;
            },
        }
    }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
    /*导航*/
    .navArea{width: 100%;height: 120px;position: fixed;left: 0;top:0;z-index: 2;}
    .navArea .logo{margin: 28px 80px;}
    .navArea .navFloatRight{width: 700px;float: right;margin-right: 0px;margin-top: 32px;}
    .navArea .navFloatRight li{float: left;margin-right: 50px;position: relative}
    .navArea .navFloatRight li .bgNavItem{display: inline-block;height: 50px;line-height: 50px;font-size: 14px;color:#222;position: relative;margin-top: -5px;}
    .navArea .navFloatRight li .bgNavItem:after {position: absolute;width: 0%;content: '';border-bottom: 3px solid #3ED8C4;bottom: 0px;left: 0;}
    .navArea .navFloatRight li .bgNavItem:hover{color:rgba(62,216,196,1);}
    .navArea .navFloatRight li .bgNavItem:hover:after {width: 100%;
        transition:width 0.4s;
        -moz-transition:width 0.4s; /* Firefox 4 */
        -webkit-transition:width 0.4s; /* Safari and Chrome */
        -o-transition:width 0.4s; /* Opera */
        transition-timing-function: linear;
    }
    .navArea .navFloatRight li .goPage.router-link-active .bgNavItem{display: inline-block; color: #3ED8C4;}
    .navArea .navFloatRight li .goPage.router-link-active .btmLine{display: block;border-bottom: 3px solid #3ED8C4;margin-top: -3px;}

    .navArea .navFloatRight .userDynamicsNav .childGoPage{display: none; width: 140px;height: 152px;background:rgba(62,215,195,1); box-shadow:0px 0px 0px rgba(0,0,0,0.16);text-align: center;position: absolute;left: -40px;top:40px;}
    .navArea .navFloatRight .userDynamicsNav .childGoPage  .childPage {display: block;opacity: .9}
    .navArea .navFloatRight .userDynamicsNav .childGoPage  .childPage:hover{background-color: #38cdba;opacity: 1;}
    .navArea .navFloatRight .userDynamicsNav .childGoPage  .childPage .lineTop{display: block;width:140px;height:1px;background:rgba(251,251,251,1);opacity:0.1;}
    .navArea .navFloatRight .userDynamicsNav .childGoPage  .childPage .linebtm{display: block;width:140px;height:1px;background:rgba(251,251,251,1);opacity:0.1;}
    .navArea .navFloatRight .userDynamicsNav .childGoPage  .childPage .bgNavItemTwo{font-size: 14px;color:rgba(255,255,255,1);line-height: 50px;}
    .navArea .navFloatRight .userDynamicsNav:hover .childGoPage{display: block;animation:fadeInLeft 0.5s;}

    /*登录状态*/
    .navArea .showLoginWord{width:94px;height:36px; line-height:36px;text-align:center;background:rgba(62,216,196,1);font-size: 14px;color: #fff; margin-top: 5px;cursor: pointer;}
    .navArea .showLoginIcon{width: 44px;height: 44px;border-radius: 50%;margin-top: 1px;}
    .navArea .showLoginIcon .alreadyLogin{width: 44px;height: 44px;border-radius: 50%;background-size: cover;}
    .navArea .showLoginWord:hover{background-color: #38cdba;}

    /*导航滚动后样式*/
    .navArea.Fixed{width: 100%;height: 80px;position: fixed;z-index: 2;background-color: #fff;top:0;left: 0;box-shadow: 0 0 8px #e2e2e2;opacity: 1;
        animation:myfirst 0.5s;
        -moz-animation:myfirst 0.5s; /* Firefox */
        -webkit-animation:myfirst 0.5s; /* Safari and Chrome */
        -o-animation:myfirst 0.5s; /* Opera */
    }
    @keyframes myfirst
    {
        from {opacity: .3;}
        to {opacity: 1;}
    }

    @-moz-keyframes myfirst /* Firefox */
    {
        from {opacity: .3;}
        to {opacity: 1;}
    }

    @-webkit-keyframes myfirst /* Safari and Chrome */
    {
        from {opacity: .3;}
        to {opacity: 1;}
    }

    @-o-keyframes myfirst /* Opera */
    {
        from {opacity: .3;}
        to {opacity: 1;}
    }

    .navArea.Fixed .logo{margin: 10px 80px;}
    .navArea.Fixed .navFloatRight{width: 700px;float: right;margin-right: 0px;margin-top: 0;}
    .navArea.Fixed .navFloatRight li{float: left;margin-right: 50px;position: relative;}
    .navArea.Fixed .navFloatRight li .bgNavItem{display: inline-block;height: 80px;line-height: 80px;font-size: 14px;color:#222;position: relative;margin-top: -5px;}
    .navArea.Fixed .navFloatRight li .bgNavItem:after {position: absolute;width: 0%;content: '';border-bottom: 3px solid #3ED8C4;bottom: -5px;left: 0;}
    .navArea.Fixed .navFloatRight li .bgNavItem:hover{color:rgba(62,216,196,1);}
    .navArea.Fixed .navFloatRight li .bgNavItem:hover:after {width: 100%;
        transition:width 0.4s;
        -moz-transition:width 0.4s; /* Firefox 4 */
        -webkit-transition:width 0.4s; /* Safari and Chrome */
        -o-transition:width 0.4s; /* Opera */
        transition-timing-function: linear;
    }
    .navArea.Fixed .navFloatRight li .goPage.router-link-active .bgNavItem{display: inline-block; color: #3ED8C4;}
    .navArea.Fixed .navFloatRight li .goPage.router-link-active .btmLine{display: block;border-bottom: 3px solid #3ED8C4;margin-top: 2px;}

    .navArea.Fixed .navFloatRight .userDynamicsNav .childGoPage{display: none; width: 140px;height: 152px;background:rgba(62,215,195,1); box-shadow:0px 0px 0px rgba(0,0,0,0.16);text-align: center;position: absolute;left: -40px;top:76px;}
    .navArea.Fixed .navFloatRight .userDynamicsNav .childGoPage  .childPage {display: block;opacity: .9}
    .navArea.Fixed .navFloatRight .userDynamicsNav .childGoPage  .childPage:hover{background-color: #38cdba;opacity: 1;}
    .navArea.Fixed .navFloatRight .userDynamicsNav .childGoPage  .childPage .lineTop{display: block;width:140px;height:1px;background:rgba(251,251,251,1);opacity:0.1;}
    .navArea.Fixed .navFloatRight .userDynamicsNav .childGoPage  .childPage .linebtm{display: block;width:140px;height:1px;background:rgba(251,251,251,1);opacity:0.1;}
    .navArea.Fixed .navFloatRight .userDynamicsNav .childGoPage  .childPage .bgNavItemTwo{font-size: 14px;color:rgba(255,255,255,1);line-height: 50px;}
    .navArea.Fixed .navFloatRight .userDynamicsNav:hover .childGoPage{display: block;animation:fadeInLeft 0.5s;}

    /*导航滚动后登录状态*/
    .navArea.Fixed .showLoginWord{width:94px;height:36px; line-height:36px;text-align:center;background:rgba(62,216,196,1);font-size: 14px;color: #fff; margin-top: 22px;cursor: pointer;}
    .navArea.Fixed .showLoginIcon{width: 44px;height: 44px;border-radius: 50%;margin-top: 18px;}
    .navArea.Fixed .showLoginIcon .alreadyLogin{width: 44px;height: 44px;border-radius: 50%;background-size: cover;}
    .navArea.Fixed .showLoginWord:hover{background-color: #38cdba;}
</style>
