<!--
   开发者：い 狂奔的蜗牛
   说明：程序通知
   版本：V 0.0.1
  -->

<!--html-->
<template>
    <div class="notification">
        <transition
            v-on:after-leave="afterLeave"
            enter-active-class="animated-notification slideInDown-notification "
            leave-active-class="animated-notification slideOutUp-notification "
        >
            <div class="notification-container" v-show="isShow">
                <div class="notification-icon-title-btn">
                    <img v-if="obj.icon" :src="obj.icon">
                    <div>{{obj.title}}</div>
                    <span @click="clickNow" >{{obj.btnText?obj.btnText:'现在'}}</span>
                </div>
                <div class="notification-subtitle">{{obj.subtitle}}</div>
                <div class="notification-content">{{obj.content}}</div>
            </div>
        </transition>
    </div>

</template>

<!--script-->
<script type="text/ecmascript-6">
    export default {
        data(){
            return {
                isShow: false,
                obj: {},
                timer: undefined,
                isClick: false
            }
        },
        methods: {
            show(obj){
                this.obj = obj;
                this.isClick = false;
                this.isShow = true;
                if (this.timer)
                    clearTimeout(this.timer)
                this.timer = setTimeout(() => {
                    this.isShow = false;
                }, 5000)
            },
            clickNow(){
                if (this.timer)
                    clearTimeout(this.timer)
                this.isClick = true;
                this.isShow = false;
            },
            afterLeave(){
                if (this.isClick && this.obj.callback) {
                    this.obj.callback();
                }
            }
        }
    }

</script>

<!--css-->
<style lang="stylus" rel="stylesheet/stylus" type="text/stylus">
    .slideInDown-notification
        -webkit-animation-name: slideInDown-notification
        animation-name: slideInDown-notification

    .slideOutUp-notification
        -webkit-animation-name: slideOutUp-notification
        animation-name: slideOutUp-notification

    @-webkit-keyframes slideInDown-notification
        from
            -webkit-transform: translate3d(0, -100%, 0)
            transform: translate3d(0, -100%, 0)
            visibility: visible
        to
            -webkit-transform: translate3d(0, 0, 0)
            transform: translate3d(0, 0, 0)

    @keyframes slideInDown-notification
        from
            -webkit-transform: translate3d(0, -100%, 0)
            transform: translate3d(0, -100%, 0)
            visibility: visible
        to
            -webkit-transform: translate3d(0, 0, 0)
            transform: translate3d(0, 0, 0)

    @-webkit-keyframes slideOutUp-notification
        from
            -webkit-transform: translate3d(0, 0, 0)
            transform: translate3d(0, 0, 0)
        to
            visibility: hidden
            -webkit-transform: translate3d(0, -100%, 0)
            transform: translate3d(0, -100%, 0)

    @keyframes slideOutUp-notification
        from
            -webkit-transform: translate3d(0, 0, 0)
            transform: translate3d(0, 0, 0)
        to
            visibility: hidden
            -webkit-transform: translate3d(0, -100%, 0)
            transform: translate3d(0, -100%, 0)

    .notification
        .animated-notification
            -webkit-animation-duration 0.4s
            animation-duration 0.4s
            -webkit-animation-fill-mode both
            animation-fill-mode both

    .notification
        .notification-container
            position fixed
            top 10px
            left 10px
            right 10px
            background: #fff
            z-index 2147483647
            border-radius 10px
            box-shadow 0 0 10px #D3D3D3
            .notification-icon-title-btn
                padding 10px
                display flex
                & > img
                    flex 0 0 20px
                    width 20px
                    height 20px
                    border-radius 50%
                    margin-right 10px
                & > div
                    flex 1
                    text-align left
                    font-size 16px
                    margin-top 3px
                & > span
                    padding 0 10px
                    font-size 14px
                    margin-top 4px
                    color #666
                    padding-right 0
                    text-align right
                    &:active
                        background: #f7f7f7

            .notification-subtitle
                font-size 16px
                font-weight bold
                padding 0 10px
                padding-top 3px
            .notification-content
                padding 10px
                padding-top 5px
                font-size 14px
                line-height 18px
</style>
