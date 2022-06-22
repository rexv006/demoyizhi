<template>
    <view >
		<u-row customStyle="margin-bottom: 10px">
		         <u-col span="0.5" offset="0.4">
		            <u--image :showLoading="true" :src="src" width="80px" height="80px" @click="click"></u--image>
		        </u-col>
		        <u-col span="1">
		            <u--text text="EasyKnow" size="30px"></u--text>
		        </u-col>
				<u-col span="2" offset="1.5">
					    <u-grid :border="false" @click="click">
					        <u-grid-item v-for="(baseListItem,baseListIndex) in baseList" :key="baseListIndex">
					            <text class="grid-text">{{baseListItem.title}}</text>
					        </u-grid-item>
					    </u-grid>
					    <u-toast ref="uToast" />
				</u-col>
				<u-col span="3" offset="1">
					    <u-search placeholder="请输入搜索内容" v-model="keyword"></u-search>
				</u-col>
					<u-col span="0.2" offset="1.5">
						<u-avatar :src="src" @click="pagemy"></u-avatar>
					</u-col>
					<u-col span="2.8">
						<u--text text="个人主页" size="10px" @click="pagemy"></u--text>
					</u-col>
		        </u-row>
		<view class="flex-col explore">
        <u-section class="section" title="用户推荐" :showLine="false"></u-section>
        <view class="flex-row wrapper">
            <view class="flex-col wraper-col">
                <u-avatar class="avatar" :size="23.828"></u-avatar><text class="user-nickname">
                    用户昵称:
                </text>
            </view>
            <view class="flex-col wraper-col">
                <u-avatar class="avatar" :size="23.828"></u-avatar><text class="user-nickname">
                    用户昵称:
                </text>
            </view>
            <view class="flex-col wraper-col">
                <u-avatar class="avatar" :size="23.828"></u-avatar><text class="user-nickname">
                    用户昵称:
                </text>
            </view>
            <view class="flex-col wraper-col">
                <u-avatar class="avatar" :size="23.828"></u-avatar><text class="user-nickname">
                    用户昵称:
                </text>
            </view>
            <view class="flex-col wraper-col-two">
                <u-avatar class="avatar" :size="23.828"></u-avatar><text class="user-nickname">
                    用户昵称:
                </text>
            </view>
        </view>
        <u-section class="section-two" title="热门动态" :showLine="false"></u-section>
        <view class="flex-row wrapper-two">
            <view class="flex-col wraper-col-three">
                <view class="flex-row box">
                    <u-avatar :size="11.719"></u-avatar><text class="friend-zhang-sanfeng">
                        用户昵称
                    </text>
                    <view class="u-line-1 text">今日份动态</view>
                </view>
                <u-image class="image" src="http://layui.shagua.wiki/img/4f2bbae447d426c9.png" width="92.188rpx" height="105.078rpx" :border-radius="20"></u-image>
                <view class="u-line-1 text-two">完美夏装女款爆款情趣十足2022最新速抢</view>
            </view>
            <view class="flex-col wraper-col-four">
                <u-avatar class="avatar-two" :size="11.719"></u-avatar>
                <view class="u-line-1 text-three">今日份动态<</view><text class="friend-zhang-sanfeng-two">
                    用户昵称
                </text>
                <u-image class="image" src="http://layui.shagua.wiki/img/4f2bbae447d426c9.png" width="92.188rpx" height="105.078rpx" :border-radius="20"></u-image>
                <view class="u-line-1 text-four">完美夏装女款爆款情趣十足2022最新速抢</view>
            </view>
        </view>
		<u-section class="section-three" title="热门资讯" :showLine="false"></u-section>
		<view style="margin-left: 6%;">
			<!-- 刷新页面后的顶部提示框 -->
			<view class="tips" :class="{ 'tips-ani': tipShow }">为您更新了10条最新新闻动态</view>
			<unicloud-db ref="udb" v-slot:default="{data, loading, error, options}" :options="formData" :collection="collection"
			 :field="field" @load="load">
				<!-- 基于 uni-list 的页面布局 -->
				<uni-list>
					<!-- to属性：将新闻ID和标题传给详情页 -->
					<!-- TODO：需增加日期格式化的示例 -->
					<uni-list-item direction="row" v-for="item in data" :key="item.id" :title="item.title" :to="'/pages/detail/e?id='+item._id+'&title='+item.title">
						<!-- 通过body插槽定义列表内容显示 -->
						<template v-slot:body>
							<view class="uni-list-box uni-content">
								<view class="uni-title uni-ellipsis-2" @click="pageto">{{item.title}}</view>
								<view class="uni-note">
									<text>{{item.user_name}}</text>
									<text>{{item.last_modify_date}}</text>
								</view>
							</view>
						</template>
						<!-- 通过footer插槽自定义图片右侧显示 -->
						<template v-slot:footer>
							<view class="uni-thumb" style="margin: 0;">
								<!-- 当前判断长度只为简单判断类型，实际业务中，根据逻辑直接渲染即可 -->
								<image :src="item.avatar.length > 3?item.avatar : item.avatar[0]" mode="aspectFill"></image>
							</view>
						</template>
					</uni-list-item>
				</uni-list>
				<!-- 通过 loadMore 组件实现上拉加载效果，如需自定义显示内容，可参考：https://ext.dcloud.net.cn/plugin?id=29 -->
				<uni-load-more v-if="loading || options.status === 'noMore' " :status="options.status" />
			</unicloud-db>
		</view>
		</view>
    </view>
</template>
<script>
    export default {
        data() {
            return {
				src: '/static/logo.png',
				keyword: '',
				collection: 'opendb-news-articles',
				// 查询字段，多个字段用 , 分割
				field: '_id,mode,avatar,title,user_name,excerpt,last_modify_date',
				formData: {
					status: 'loading', // 加载状态
				},
				tipShow: false ,// 是否显示顶部提示框
				baseList: [
					{
						title: '资讯'
					},
					{
						title: '社区'
					},
					{
						title: '探索'
					},
				],
				list1: [
					{
						name: '关注',
					}, 
					{
				        name: '推荐',
				    }
				],
			}
        },
		onLoad() {
			this.loadmore()
		},
        methods: {
			load(data, ended) {
				if (ended) {
					this.formData.status = 'noMore'
				}
			},
			click() {
				
			},
			scrolltolower() {
				this.loadmore()
			},
			loadmore() {
				for (let i = 0; i < 30; i++) {
					this.indexList.push({
						url: this.urls[uni.$u.random(0, this.urls.length - 1)]
					})
				}
			},

        },
		onPullDownRefresh() {
				this.formData.status = 'more'
				this.$refs.udb.loadData({
					clear: true
				}, () => {
					this.tipShow = true
					clearTimeout(this.timer)
					this.timer = setTimeout(()=>{
						this.tipShow  = false
					},1000)
					uni.stopPullDownRefresh()
				})
			},
			onReachBottom() {
				this.$refs.udb.loadMore()
			},
		};
</script>
<style lang="scss" scoped>
    /** 全局样式-开始,建议放在公共css样式文件中,比如common.css 或app.vue文件 */
@import '@/common/uni-ui.scss';
	*{
		margin: 0;
		padding: 0;
	}
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
	.wrapper {
	width: 180.908rpx;
	padding: 372.07rpx 0rpx 90.82rpx 0rpx;
	}
	
	.swiper {
		width: 100%;
		margin-bottom: 16.113rpx;
	}
	
	.text {
		width: 100%;
	}
	.wrap {
	    padding: 12px;
	}
	
	.demo-layout {
	    height: 25px;
	    border-radius: 4px;
	}
	
	.bg-purple {
	    background: #CED7E1;
	}
	
	.bg-purple-light {
	    background: #e5e9f2;
	}
	
	.bg-purple-dark {
	    background: #99a9bf;
	}
	
	.uni-list-box {
		margin-top: 0;
	}
	
	.uni-content {
		padding-right: 10px;
	}
	
	.uni-note {
		display: flex;
		margin: 0;
		justify-content: space-between;
	}
	
	.tips {
		color: #67c23a;
		font-size: 14px;
		line-height: 40px;
		text-align: center;
		background-color: #f0f9eb;
		height: 0;
		opacity: 0;
		transform: translateY(-100%);
		transition: all 0.3s;
	}
	
	.tips-ani {
		transform: translateY(0);
		height: 40px;
		opacity: 1;
	}
	
	.content {
		width: 100%;
		display: flex;
	}
	
	.list-picture {
		width: 100%;
		height: 145px;
	}
	
	.thumb-image {
		width: 100%;
		height: 100%;
	}
	
	.ellipsis {
		display: flex;
		overflow: hidden;
	}
	
	.uni-ellipsis-1 {
		overflow: hidden;
		white-space: nowrap;
		text-overflow: ellipsis;
	}
	
	.uni-ellipsis-2 {
		overflow: hidden;
		text-overflow: ellipsis;
		display: -webkit-box;
		-webkit-line-clamp: 2;
		-webkit-box-orient: vertical;
	}
    .explore {
        height: 1080px;
        padding-top: 10px;

        .section {
            width: 1410px;
            height: 38px;
            margin: 0px 0px 3px 99px;
        }

        .wrapper {
            width: 1314px;
            justify-content: space-between;
            margin: 0px 0px 5px 99px;
            padding: 13px 247px 10px 21px;

            .wraper-col {
                width: 162px;
                height: 164px;
                padding: 23px 50.5px 0px 50.5px;

                .avatar {
                    margin-bottom: 20px;
                }

                .user-nickname {
                    width: 60px;
                    font-size: 14px;
                    line-height: 14px;
                }
            }

            .wraper-col-two {
                width: 162px;
                height: 164px;
                padding: 24px 50.5px 0px 50.5px;

                .avatar {
                    margin-bottom: 20px;
                }

                .user-nickname {
                    width: 60px;
                    font-size: 14px;
                    line-height: 14px;
                }
            }
        }

        .section-two {
            width: 1410px;
            height: 38px;
            margin: 0px 0px 13px 99px;
        }

        .wrapper-two {
            width: 1920px;
            justify-content: space-between;
            margin-bottom: 10px;
            padding: 0px 1154px 0px 99px;

            .wraper-col-three {
                width: 303px;
                padding: 15px 0px 6px 15px;
                background: #FFFFFF;

                .box {
                    width: 235px;
                    justify-content: space-between;
                    margin-bottom: 22px;

                    .friend-zhang-sanfeng {
                        margin-top: 6px;
                        font-size: 12px;
                        color: #fa3534;
                    }

                    .text {
                        width: 120px;
                        margin-top: 6px;
                        font-size: 12px;
                    }
                }

                .image {
                    margin: 0px 0px 21px 29px;
                }

                .text-two {
                    width: 167px;
                    font-weight: 600;
                }
            }

            .wraper-col-four {
                width: 303px;
                padding: 15px 0px 6px 15px;
                background: #FFFFFF;

                .avatar-two {
                    margin-bottom: -24px;
                }

                .text-three {
                    width: 120px;
                    margin: 0px 0px -18px 115px;
                    font-size: 12px;
                }

                .friend-zhang-sanfeng-two {
                    width: 63px;
                    margin: 0px 0px 28px 44px;
                    font-size: 12px;
                    color: #fa3534;
                }

                .image {
                    margin: 0px 0px 21px 29px;
                }

                .text-four {
                    width: 167px;
                    font-weight: 600;
                }
            }
        }

        .section-three {
            width: 1410px;
            height: 38px;
            margin-left: 92px;
        }
    }
</style>