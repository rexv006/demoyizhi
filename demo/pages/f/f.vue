<template>
    <view class="flex-col homepage">
        <view class="flex-row wrapper">
            <view class="flex-row wraper-col">
                <u-icon class="icon-u" :name="data5" :size="80" label="科学技术" :label-size="30" label-color="#2b85e4" label-pos="bottom"></u-icon>
                <view class="u-line-1 text">超过宽度自动换行,超过高度自动隐藏不溢出;超过宽度自动换行,超过高度自动隐藏不溢出;超过宽度自动换行,超过高度自动隐藏不溢出;是日也，天朗气清，惠风和畅，仰观宇宙之大，俯察品类之盛，所以游目骋怀，足以极视听之娱，信可乐也;是日也，天朗气清，惠风和畅，仰观宇宙之大，俯察品类之盛，所以游目骋怀，足以极视听之娱，信可乐也</view>
            </view>
            <u-search class="search" v-model="form['searchValue']"></u-search>
            <u-avatar class="avatar" :size="24.902"></u-avatar>
        </view>
        <view class="flex-row wrapper-two">
            <u-image src="https://vkceyugu.cdn.bspapp.com/VKCEYUGU-55dbb834-9ba8-4068-98ca-c341f6402e27/69f5dc05-effa-4a05-b56c-7185a5b73dca.png" width="80.566rpx" height="76.904rpx" shape="circle"></u-image>
            <u-parse class="parse" html="
					<p>露从今夜白，月是故乡明</p>
					<p style='color:red'>露从今夜白，月是故乡明</p>
				"></u-parse>
        </view>
        <u-tabs class="tabs" :list="list" :current="currentTabIndex" @change="tabsChange"></u-tabs>
        <u-card class="card" margin="0rpx 0rpx 0rpx 72.51rpx">
            <view class="" slot="body">
                <view class="u-body-item u-flex u-border-bottom u-col-between u-p-t-0">
                    <view class="u-body-item-title u-line-2"> 瓶身描绘的牡丹一如你初妆，冉冉檀香透过窗心事我了然，宣纸上走笔至此搁一半 </view>
                    <image class="u-body-item-image" src="https://img11.360buyimg.com/n7/jfs/t1/94448/29/2734/524808/5dd4cc16E990dfb6b/59c256f85a8c3757.jpg" mode="aspectFill"></image>
                </view>
                <view class="u-body-item u-flex u-row-between u-p-b-0">
                    <view class="u-body-item-title u-line-2"> 釉色渲染仕女图韵味被私藏，而你嫣然的一笑如含苞待放 </view>
                    <image class="u-body-item-image" src="https://img12.360buyimg.com/n7/jfs/t1/102191/19/9072/330688/5e0af7cfE17698872/c91c00d713bf729a.jpg" mode="aspectFill"></image>
                </view>
            </view>
            <view class="" slot="foot">
                <u-icon name="chat-fill" size="34" label="30评论"></u-icon>
            </view>
        </u-card>
    </view>
</template>
<script>
    export default {
        data() {
            return {
                currentTabIndex: 0,
                data5: "https://renxingbuju.oss-cn-shenzhen.aliyuncs.com/images/2021/10/20/image_1634742906_Go7Okkfo.png",
                form: {
                    searchValue: ""
                },
                list: [{
                    name: "待收货"
                }, {
                    name: "待付款"
                }, {
                    name: "待评价",
                    count: 5
                }]
            }
        },
        methods: {
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

    .homepage {
        height: 585.205rpx;
        padding: 21.973rpx 0rpx 0rpx 21.24rpx;

        .wrapper {
            width: 619.629rpx;
            margin-bottom: 23.438rpx;

            .wraper-col {
                width: 139.16rpx;
                margin-right: 30.029rpx;

                .icon-u {
                    margin-right: -5.859rpx;
                }

                .text {
                    width: 101.074rpx;
                    margin-top: 11.719rpx;
                }
            }

            .search {
                width: 324.463rpx;
                margin: 8.789rpx 101.074rpx 0rpx 0rpx;
                flex: 0;
            }

            .avatar {
                margin-top: 8.789rpx;
            }
        }

        .wrapper-two {
            width: 401.367rpx;
            justify-content: space-between;
            margin: 0rpx 0rpx 16.846rpx 209.473rpx;

            .parse {
                width: 283.447rpx;
                height: 122.314rpx;
                margin-top: 6.592rpx;
            }
        }

        .tabs {
            width: 529.541rpx;
            height: 24.902rpx;
            margin: 0rpx 0rpx 33.691rpx 57.129rpx;
        }

        .card {
            width: 562.5rpx;
        }
    }

    .u-body-item {
        font-size: 32rpx;
        color: #333;
        padding: 20rpx 10rpx;
    }

    .u-body-item-image {
        width: 120rpx;
        flex: 0 0 120rpx;
        height: 120rpx;
        border-radius: 8rpx;
        margin-left: 12rpx;
    }
</style>