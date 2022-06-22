<template>
    <view class="flex-col h">
        <view class="flex-col wrapper">
            <view class="flex-row wraper-row">
                <u-avatar class="avatar" :size="44.678"></u-avatar><text class="my-order">
                    我的订单
                </text> <text class="user-nickname">
                    用户昵称:
                </text>
                <u-button class="button" type="success" size="mini">
                    按钮
                </u-button>
            </view>
            <u-alert-tips class="alertTips" title="寻隐者不遇" description="松下问童子，言师采药去。只在此山中，云深不知处。"></u-alert-tips>
        </view>
        <view class="flex-row wrapper-two">
            <view class="flex-col wraper-col">
                <u-tabs class="tabs" :list="list" :current="currentTabIndex" @change="tabsChange"></u-tabs>
                <u-collapse class="collapse">
                    <u-collapse-item :title="item.head" v-for="(item, index) in citemList" :key="index" :open="item.open" :disabled="item.disabled"> {{item.body}} </u-collapse-item>
                </u-collapse>
                <u-swiper class="swiper" :list="list2"></u-swiper>
            </view>
            <view class="flex-col wraper-col-two">
                <u-section class="section" title="今日热门"></u-section>
                <view class="swipeAction">
                    <u-swipe-action :options="options" v-for="(item, index) in swipeActionlist" :key="item.id" :index="index" @click="click" @open="open">
                        <view class="item u-border-bottom">
                            <image class="image" mode="aspectFill" :src="item.images" /> <!-- 此层wrap在此为必写的，否则可能会出现标题定位错误 -->
                            <view class="title-wrap"> <text class="title u-line-2">{{ item.title }}</text> </view>
                        </view>
                    </u-swipe-action>
                </view>
            </view>
        </view>
    </view>
</template>
<script>
    export default {
        data() {
            return {
                citemList: [{
                    head: "赏识在于角度的转换",
                    body: "只要我们正确择取一个合适的参照物乃至稍降一格去看待他人，值得赏识的东西便会扑面而来",
                    open: true,
                    disabled: false
                }, {
                    head: "生活中不是缺少美，而是缺少发现美的眼睛",
                    body: "学会欣赏，实际是一种积极生活的态度，是生活的调味品，会在欣赏中发现生活的美",
                    open: false
                }, {
                    head: "周围一些不起眼的人、事、物，或许都隐藏着不同凡响的智慧",
                    body: "但是据说雕刻大卫像所用的这块大理石，曾被多位雕刻家批评得一无是处，有些人认为这块大理石采凿得不好，有些人嫌它的纹路不够美",
                    open: false
                }],
                currentTabIndex: 2,
                list: [{
                    name: "待收货"
                }, {
                    name: "待付款"
                }, {
                    name: "待评价",
                    count: 5
                }],
                list2: [{
                    image: "https://cdn.uviewui.com/uview/swiper/1.jpg",
                    title: "昨夜星辰昨夜风，画楼西畔桂堂东"
                }, {
                    image: "https://cdn.uviewui.com/uview/swiper/2.jpg",
                    title: "身无彩凤双飞翼，心有灵犀一点通"
                }, {
                    image: "https://cdn.uviewui.com/uview/swiper/3.jpg",
                    title: "谁念西风独自凉，萧萧黄叶闭疏窗，沉思往事立残阳"
                }],
                options: [{
                    text: "收藏",
                    style: {
                        backgroundColor: "#007aff",
                        width: "180rpx"
                    }
                }, {
                    text: "删除",
                    style: {
                        backgroundColor: "#dd524d",
                        width: "180rpx"
                    }
                }],
                swipeActionlist: [{
                    id: 1,
                    title: "长安回望绣成堆，山顶千门次第开，一骑红尘妃子笑，无人知是荔枝来",
                    images: "https://cdn.uviewui.com/uview/common/logo.png",
                    show: false
                }, {
                    id: 2,
                    title: "新丰绿树起黄埃，数骑渔阳探使回，霓裳一曲千峰上，舞破中原始下来",
                    images: "https://cdn.uviewui.com/uview/common/logo.png",
                    show: false
                }, {
                    id: 3,
                    title: "登临送目，正故国晚秋，天气初肃。千里澄江似练，翠峰如簇",
                    images: "https://cdn.uviewui.com/uview/common/logo.png",
                    show: false
                }]
            }
        },
        methods: {
            click(index, index1) {
                if (index1 == 1) {
                    this.swipeActionlist.splice(index, 1);
                    this.$u.toast(`删除了第${index}个cell`);
                } else {
                    this.swipeActionlist[index].show = false;
                    this.$u.toast(`收藏成功`);
                }
            },
            open(index) {
                // 先将正在被操作的swipeAction标记为打开状态，否则由于props的特性限制，
                // 原本为'false'，再次设置为'false'会无效
                this.swipeActionlist[index].show = true;
                this.swipeActionlist.map((val, idx) => {
                    if (index != idx) this.swipeActionlist[idx].show = false;
                })
            },
            tabsChange(index) {
                this.currentTabIndex = index;
            }
        }
    }
</script>
<style lang="scss" scoped>
    /** 全局样式-开始,建议放在公共css样式文件中,比如common.css 或app.vue文件 */

    html,
    body {
        margin: 0;
        width: 100%;
        height: 100%;
        font-size: 16px
    }

    view,
    text,
    image {
        position: relative;
        box-sizing: border-box;
        flex-shrink: 0;
    }

    .flex-col {
        display: flex;
        align-items: flex-start;
        flex-direction: column;
    }

    .flex-row {
        display: flex;
        align-items: flex-start;
    }

    .flex-col .flex-row {
        width: 100%
    }

    /** 全局样式-结束*/

    .h {
        padding: 23px 0px 16px 12px;

        .wrapper {
            width: 985px;
            height: 200px;
            margin: 0px 0px 12px 1px;
            padding: 27px 5px 0px 5px;

            .wraper-row {
                width: 924px;
                margin: 0px 0px 12px 36px;

                .avatar {
                    margin-right: 13px;
                }

                .my-order {
                    margin: 18px 29px 0px 0px;
                    font-size: 18px;
                    font-weight: 600;
                }

                .user-nickname {
                    margin: 22px 645px 0px 0px;
                    font-size: 14px;
                    line-height: 14px;
                }

                .button {
                    height: 24px;
                    margin-top: 18px;
                }
            }

            .alertTips {
                width: 100%;
            }
        }

        .wrapper-two {
            width: 990px;
            justify-content: space-between;

            .wraper-col {
                width: 301px;
                height: 548px;
                padding: 9px 0px 0px 6px;

                .tabs {
                    width: 277px;
                    margin: 0px 0px 10px 4px;
                }

                .collapse {
                    width: 261px;
                    margin: 0px 0px 219px 14px;
                }

                .swiper {
                    width: 285px;
                    height: 133px;
                }
            }

            .wraper-col-two {
                width: 679px;
                height: 543px;
                padding: 15px 9.5px 0px 9.5px;

                .section {
                    width: 100%;
                    margin-bottom: 8px;
                }

                .swipeAction {
                    width: 656px;
                    margin-right: auto;
                    margin-left: auto;
                    flex: 0;
                }
            }
        }
    }

    .item {
        display: flex;
        padding: 20rpx;
    }

    .image {
        width: 120rpx;
        flex: 0 0 120rpx;
        height: 120rpx;
        margin-right: 20rpx;
        border-radius: 12rpx;
    }

    .title {
        text-align: left;
        font-size: 28rpx;
        color: $u-content-color;
        margin-top: 20rpx;
    }
</style>