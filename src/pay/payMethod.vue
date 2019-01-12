<template>
    <div class="payMethodContainer">

        <section class="pay_way container_style">
            <header class="header_style">
                <span>支付方式</span>
                <div class="more_type" @click="showPayWayFun">
                    <span v-if="!payWayName">{{payMethodList[0].name}}</span>
                    <span v-if="payWayName">{{this.payWayName}}</span>
                    <svg class="address_empty_right">
                        <use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#arrow-right"></use>
                    </svg>
                </div>
            </header>
        </section>
        <transition name="slid_up">
            <div class="choose_type_Container" v-if="showPayWay">
                <header>支付方式</header>
                <ul>
                    <li v-for="item in payMethodList" :key="item.id" :class="{choose: payWayId==item.id}">
                        <span>{{item.name}}</span>
                        <svg class="address_empty_right" @click="choosePayWay(item)">
                            <use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#select"></use>
                        </svg>
                    </li>
                </ul>
            </div>
        </transition>
        <svg-icon></svg-icon>
     </div>
     
</template>

<script>
import svgIcon from '../common/svg';
export default {
  name: "payMethod",
  components: {
      svgIcon
    //payMethod
  },
  data () {
    return {
        showPayWay: false,// 显示付款方式
        payWayId:this.payMethodList[0].id, // 默认第一个付款方式
        payWayName:""   // 付款名字
    }
  },
  props: {
    // 传入付款方式数据参数 
    payMethodList: {
      type: Array,
      required: true,
      default: [{}]
    }
  },
  mounted() {
      // 默认传值 第一种付款方式
      this.initData()
  },
  methods:{
        initData(){
            this.$emit("payWayId",this.payWayId)
        },
        // 显示付款方式
        showPayWayFun(){
            this.showPayWay = !this.showPayWay
        },
        // 点击选择付款方式
        choosePayWay(item){
            this.payWayName = item.name
            this.payWayId = item.id
            this.showPayWay = !this.showPayWay

            // 返回数据
            this.$emit("payWayId",this.payWayId)
        },
    },
}
</script>

<style lang="scss" scoped>
    @import '../mixin';

    .payMethodContainer{
        padding-top: 1.95rem;
        padding-bottom: 3rem;
        p, span{
            font-family: Helvetica Neue,Tahoma,Arial;
        }
    }
    .container_style{
        background-color: #fff;
        margin-top: .4rem;
        padding: 0 .7rem;
    }
    .slid_up-enter-active, .slid_up-leave-active {
        transition: all .3s;
    }
    .slid_up-enter, .slid_up-leave-active {
        transform: translate3d(0,10rem,0)
    }
    .pay_way{
        .header_style{
            @include fj;
            line-height: 2rem;
            span:nth-of-type(1){
                @include sc(.7rem, #666);
            }
            .more_type{
                span:nth-of-type(1){
                    @include sc(.6rem, #aaa);
                    width: 10rem;
                    display: inline-block;
                    text-align: right;
                    vertical-align: middle;
                }
                svg{
                    @include wh(.5rem, .5rem);
                    fill: #ccc;
                }
            }
        }
        .support_is_available{
            span{
                color: #666;
            }
        }
    }
    .address_empty_right{
        @include wh(.6rem, .6rem);
        fill: #999;
    }
    .address_empty_right{
        @include wh(.6rem, .6rem);
        fill: #999;
    }
    .choose_type_Container{
        min-height: 10rem;
        background-color: #fff;
        position: fixed;
        bottom: 0;
        width: 100%;
        z-index: 204;
        header{
            background-color: #fafafa;
            @include sc(.7rem, #333);
            text-align: center;
            line-height: 2rem;
        }
        ul{
            li{
                @include fj;
                padding: 0 .7rem;
                line-height: 2.5rem;
                align-items: center;
                span{
                    @include sc(.7rem, #ccc);
                }
                svg{
                    @include wh(.8rem, .8rem);
                    fill: #eee;
                }
            }
            .choose{
                span{
                    color: #333;
                }
                svg{
                    fill: #4cd964;
                }
            }
        }
    }
</style>