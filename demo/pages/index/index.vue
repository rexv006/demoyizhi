<template>
    <view class="u-page">
            <view class="u-demo-block">
                <view class="u-demo-block__content">
                    <u-row customStyle="margin-bottom: 10px">
                        <u-col span="0.5" offset="0.4">
                            <u--image :showLoading="true" :src="src" width="80px" height="80px" @click="click"></u--image>
                        </u-col>
                        <u-col span="1">
                            <u--text text="EasyKnow" size="30px"></u--text>
                        </u-col>
						<u-col span="2" offset="1.5">
						    <u-grid :border="false">
						        <u-grid-item v-for="(baseListItem,baseListIndex) in baseList" :key="baseListIndex">
						            <text class="grid-text" @click="click(baseListItem.Text)">{{baseListItem.title}}</text>
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
                    <u-row customStyle="margin-bottom: 10px">
                        <u-col span="8" offset="1">
							<u-row>
								<u-tabs :list="list1" @click=""></u-tabs>
							</u-row>
							<u-row>
								<ul id="example-1">
									<view>
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
									<!-- <li style="list-style:none; padding-top: 30px; padding-left: 10px;">
										<u-row>
											<u-col span="2.5">
												<u--image :showLoading="true" src="/static/1.png" width="180px" height="90px" radius="10px" @click="click"></u--image>
											</u-col>
											<u-col span="8">
												<h2>2022中国大学排名</h2>
												<view style="margin-top: 10px;">
												<u--text :lines="2" text="“软科中国大学排名”前身是“中国最好大学排名”，自2015年首次发布以来，以专业、客观、透明的优势赢得了高等教育领域内外的广泛关注和认可，已经成为具有重要社会影响力和权威参考价值的中国大学排名领先品牌。软科中国大学排名以服务中国高等教育发展和进步为导向，依托自主研发的高等教育评价专利技术和“大学360度数据监测平台”的大数据支持，采用数百项指标变量对中国大学进行全方位、体系化、监测式评价，向学生、家长和全社会提供及时、可靠、丰富的高校可比信息（查看排名方法）。"></u--text>
												</view>
											</u-col>
										</u-row>
									</li>
									<li style="list-style:none; padding-top: 30px; padding-left: 10px;">
										<u-row>
											<u-col span="2.5">
												<u--image :showLoading="true" src="/static/1.png" width="180px" height="90px" radius="10px" @click="click"></u--image>
											</u-col>
											<u-col span="8">
												<h2>2022中国大学排名</h2>
												<view style="margin-top: 10px;">
												<u--text :lines="2" text="“软科中国大学排名”前身是“中国最好大学排名”，自2015年首次发布以来，以专业、客观、透明的优势赢得了高等教育领域内外的广泛关注和认可，已经成为具有重要社会影响力和权威参考价值的中国大学排名领先品牌。软科中国大学排名以服务中国高等教育发展和进步为导向，依托自主研发的高等教育评价专利技术和“大学360度数据监测平台”的大数据支持，采用数百项指标变量对中国大学进行全方位、体系化、监测式评价，向学生、家长和全社会提供及时、可靠、丰富的高校可比信息（查看排名方法）。"></u--text>
												</view>
											</u-col>
										</u-row>
									</li>
									<li style="list-style:none; padding-top: 30px; padding-left: 10px;">
										<u-row>
											<u-col span="2.5">
												<u--image :showLoading="true" src="/static/1.png" width="180px" height="90px" radius="10px" @click="click"></u--image>
											</u-col>
											<u-col span="8">
												<h2>2022中国大学排名</h2>
												<view style="margin-top: 10px;">
												<u--text :lines="2" text="“软科中国大学排名”前身是“中国最好大学排名”，自2015年首次发布以来，以专业、客观、透明的优势赢得了高等教育领域内外的广泛关注和认可，已经成为具有重要社会影响力和权威参考价值的中国大学排名领先品牌。软科中国大学排名以服务中国高等教育发展和进步为导向，依托自主研发的高等教育评价专利技术和“大学360度数据监测平台”的大数据支持，采用数百项指标变量对中国大学进行全方位、体系化、监测式评价，向学生、家长和全社会提供及时、可靠、丰富的高校可比信息（查看排名方法）。"></u--text>
												</view>
											</u-col>
										</u-row>
									</li>
									<li style="list-style:none; padding-top: 30px; padding-left: 10px;">
										<u-row>
											<u-col span="2.5">
												<u--image :showLoading="true" src="/static/1.png" width="180px" height="90px" radius="10px" @click="click"></u--image>
											</u-col>
											<u-col span="8">
												<h2>2022中国大学排名</h2>
												<view style="margin-top: 10px;">
												<u--text :lines="2" text="“软科中国大学排名”前身是“中国最好大学排名”，自2015年首次发布以来，以专业、客观、透明的优势赢得了高等教育领域内外的广泛关注和认可，已经成为具有重要社会影响力和权威参考价值的中国大学排名领先品牌。软科中国大学排名以服务中国高等教育发展和进步为导向，依托自主研发的高等教育评价专利技术和“大学360度数据监测平台”的大数据支持，采用数百项指标变量对中国大学进行全方位、体系化、监测式评价，向学生、家长和全社会提供及时、可靠、丰富的高校可比信息（查看排名方法）。"></u--text>
												</view>
											</u-col>
										</u-row>
									</li>
									<li style="list-style:none; padding-top: 30px; padding-left: 10px;">
										<u-row>
											<u-col span="2.5">
												<u--image :showLoading="true" src="/static/1.png" width="180px" height="90px" radius="10px" @click="click"></u--image>
											</u-col>
											<u-col span="8">
												<h2>2022中国大学排名</h2>
												<view style="margin-top: 10px;">
												<u--text :lines="2" text="“软科中国大学排名”前身是“中国最好大学排名”，自2015年首次发布以来，以专业、客观、透明的优势赢得了高等教育领域内外的广泛关注和认可，已经成为具有重要社会影响力和权威参考价值的中国大学排名领先品牌。软科中国大学排名以服务中国高等教育发展和进步为导向，依托自主研发的高等教育评价专利技术和“大学360度数据监测平台”的大数据支持，采用数百项指标变量对中国大学进行全方位、体系化、监测式评价，向学生、家长和全社会提供及时、可靠、丰富的高校可比信息（查看排名方法）。"></u--text>
												</view>
											</u-col>
										</u-row>
									</li> -->
								</ul>
							</u-row>
							<!-- <u-list @scrolltolower="scrolltolower">
								<u-list-item v-for="(item,index) in indexList" :key="index">
									<u-cell :title="`列表-${item}`" note="lll">
										<u--text text="lljlajwd"></u--text>
									</u-cell>
								</u-list-item>
							</u-list> -->
                        </u-col>
                        <u-col span="4">
                        	<!-- <view class="flex-col wrapper">
                        	    <u-swiper class="swiper" :list="list2" ></u-swiper>
                        	    <view class="u-line-1 text"></view>
                        	</view> -->
                        </u-col>
                    </u-row>
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
						title: '资讯',
						Text:'index',
						
					},
					{
						title: '社区',
						Text:"community",
					},
					{
						title: '探索',
						Text:"explore",
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
			click(Text) {
			                uni.navigateTo(
							{
								url:"/pages/"+Text+"/"+Text
							})
			            },
			pagecomm() {
				uni.navigateTo({
					url:"/pages/community/community"
				})
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
			pageex(){
				uni.navigateTo({
					url:"/pages/explore/explore"
				})
			},
			pageto(){
				uni.navigateTo(
				{
					//url:"/pages/detail/e"
				})
			},
			pagemy(){
				uni.navigateTo(
				{
					url:"/pages/my/my"
				})
			},
			pagecom(){
				uni.navigateTo(
				{
					url:"/pages/community/community"
				})
			}
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
 

<style lang="scss">
	@import '@/common/uni-ui.scss';
	*{
		margin: 0;
		padding: 0;
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
	page {
		display: flex;
		flex-direction: column;
		box-sizing: border-box;
		background-color: #efeff4;
		min-height: 100%;
		height: auto;
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
</style>