<template>
    <view class="u-page">
            <view class="u-demo-block">
                <view class="u-demo-block__content">
                    <u-row customStyle="margin-bottom: 10px">
                        <u-col span="0.5" offset="0.4">
                            <u--image :showLoading="true" :src="src" width="80px" height="80px" @click="click('../index/index')"></u--image>
                        </u-col>
                        <u-col span="1">
                            <u--text text="EasyKnow" size="30px"></u--text>
                        </u-col>
						<u-col span="2" offset="1.5">
						    <u-grid :border="false" @click="click">
						        <u-grid-item v-for="(baseListItem,baseListIndex) in baseList" :key="baseListIndex">
						            <text @click="click(baseListItem.url)">{{baseListItem.title}}</text>
						        </u-grid-item>
						    </u-grid>
						    <u-toast ref="uToast" />
						</u-col>
						<u-col span="3" offset="1">
						    <u-search placeholder="请输入搜索内容" v-model="keyword"></u-search>
						</u-col>
						<u-col span="0.4" offset="1.2" @click="click('../my/my')">
							<u-avatar :src="src1"></u-avatar>
						</u-col>
						<u-col span="2.8" @click="click('../my/my')">
							<u--text text="Easy" size="15px"></u--text>
						</u-col>
                    </u-row>
                    <u-row customStyle="margin-bottom: 10px">
                        <u-col span="6" offset="2">
							<u-row>
								<u-tabs :list="list1" @click="click"></u-tabs>
							</u-row>
							<u-row>
								<ul id="example-1">
									<li style="list-style:none; padding-top: 30px; padding-left: 10px;">
										<view style="width: 8%; float: left; margin-top: 20px;">
											<u-row>
												<u-avatar :src="src1" shape="square"></u-avatar>
											</u-row>
										</view>
										<view style="width: 90%; float: left; margin-top: 20px;">
											<u-row customStyle="margin-top: 6px">
												<u--text text="Easy" size="25px"></u--text>
											</u-row>
											<u-row customStyle="margin-top: 15px">
												<h2 style="margin-top: 0px;">考研倒计时50天</h2>
											</u-row>
											<u-row customStyle="margin-top: 15px">
												<u--text :lines="2" text="“软科中国大学排名”前身是“中国最好大学排名”，自2015年首次发布以来，以专业、客观、透明的优势赢得了高等教育领域内外的广泛关注和认可，已经成为具有重要社会影响力和权威参考价值的中国大学排名领先品牌。软科中国大学排名以服务中国高等教育发展和进步为导向，依托自主研发的高等教育评价专利技术和“大学360度数据监测平台”的大数据支持，采用数百项指标变量对中国大学进行全方位、体系化、监测式评价，向学生、家长和全社会提供及时、可靠、丰富的高校可比信息（查看排名方法）。"></u--text>
											</u-row>
											<u-row customStyle="margin-top: 15px">
												<u--image :src="src1"></u--image>
											</u-row>
											<u-row>
												<u-grid :border="false" @click="click">
													<u-grid-item v-for="(baseListItem,baseListIndex) in list2" :key="baseListIndex">
														<u-icon
															:customStyle="{paddingTop:40+'rpx'}"
															:name="baseListItem.name"
															:size="22"
														></u-icon>
														<text class="grid-num">{{baseListItem.num}}</text>
													</u-grid-item>
												</u-grid>
												<u-toast ref="uToast" />
											</u-row>
										</view>
									</li>
									<li style="list-style:none; padding-top: 30px; padding-left: 10px;">
										<view style="width: 8%; float: left; margin-top: 20px;">
											<u-row>
												<u-avatar :src="src1" shape="square"></u-avatar>
											</u-row>
										</view>
										<view style="width: 90%; float: left; margin-top: 20px;">
											<u-row customStyle="margin-top: 6px">
												<u--text text="Easy" size="25px"></u--text>
											</u-row>
											<u-row customStyle="margin-top: 15px">
												<h2 style="margin-top: 0px;">考研倒计时50天</h2>
											</u-row>
											<u-row customStyle="margin-top: 15px">
												<u--text :lines="2" text="“软科中国大学排名”前身是“中国最好大学排名”，自2015年首次发布以来，以专业、客观、透明的优势赢得了高等教育领域内外的广泛关注和认可，已经成为具有重要社会影响力和权威参考价值的中国大学排名领先品牌。软科中国大学排名以服务中国高等教育发展和进步为导向，依托自主研发的高等教育评价专利技术和“大学360度数据监测平台”的大数据支持，采用数百项指标变量对中国大学进行全方位、体系化、监测式评价，向学生、家长和全社会提供及时、可靠、丰富的高校可比信息（查看排名方法）。"></u--text>
											</u-row>
											<u-row customStyle="margin-top: 15px">
												<u--image :src="src1"></u--image>
											</u-row>
											<u-row>
												<u-grid :border="false" @click="click">
													<u-grid-item v-for="(baseListItem,baseListIndex) in list2" :key="baseListIndex">
														<u-icon
															:customStyle="{paddingTop:40+'rpx'}"
															:name="baseListItem.name"
															:size="22"
														></u-icon>
														<text class="grid-num">{{baseListItem.num}}</text>
													</u-grid-item>
												</u-grid>
												<u-toast ref="uToast" />
											</u-row>
										</view>
									</li><li style="list-style:none; padding-top: 30px; padding-left: 10px;">
										<view style="width: 8%; float: left; margin-top: 20px;">
											<u-row>
												<u-avatar :src="src1" shape="square"></u-avatar>
											</u-row>
										</view>
										<view style="width: 90%; float: left; margin-top: 20px;">
											<u-row customStyle="margin-top: 6px">
												<u--text text="Easy" size="25px"></u--text>
											</u-row>
											<u-row customStyle="margin-top: 15px">
												<h2 style="margin-top: 0px;">考研倒计时50天</h2>
											</u-row>
											<u-row customStyle="margin-top: 15px">
												<u--text :lines="2" text="“软科中国大学排名”前身是“中国最好大学排名”，自2015年首次发布以来，以专业、客观、透明的优势赢得了高等教育领域内外的广泛关注和认可，已经成为具有重要社会影响力和权威参考价值的中国大学排名领先品牌。软科中国大学排名以服务中国高等教育发展和进步为导向，依托自主研发的高等教育评价专利技术和“大学360度数据监测平台”的大数据支持，采用数百项指标变量对中国大学进行全方位、体系化、监测式评价，向学生、家长和全社会提供及时、可靠、丰富的高校可比信息（查看排名方法）。"></u--text>
											</u-row>
											<u-row customStyle="margin-top: 15px">
												<u--image :src="src1"></u--image>
											</u-row>
											<u-row>
												<u-grid :border="false" @click="click">
													<u-grid-item v-for="(baseListItem,baseListIndex) in list2" :key="baseListIndex">
														<u-icon
															:customStyle="{paddingTop:40+'rpx'}"
															:name="baseListItem.name"
															:size="22"
														></u-icon>
														<text class="grid-num">{{baseListItem.num}}</text>
													</u-grid-item>
												</u-grid>
												<u-toast ref="uToast" />
											</u-row>
										</view>
									</li><li style="list-style:none; padding-top: 30px; padding-left: 10px;">
										<view style="width: 8%; float: left; margin-top: 20px;">
											<u-row>
												<u-avatar :src="src1" shape="square"></u-avatar>
											</u-row>
										</view>
										<view style="width: 90%; float: left; margin-top: 20px;">
											<u-row customStyle="margin-top: 6px">
												<u--text text="Easy" size="25px"></u--text>
											</u-row>
											<u-row customStyle="margin-top: 15px">
												<h2 style="margin-top: 0px;">考研倒计时50天</h2>
											</u-row>
											<u-row customStyle="margin-top: 15px">
												<u--text :lines="2" text="“软科中国大学排名”前身是“中国最好大学排名”，自2015年首次发布以来，以专业、客观、透明的优势赢得了高等教育领域内外的广泛关注和认可，已经成为具有重要社会影响力和权威参考价值的中国大学排名领先品牌。软科中国大学排名以服务中国高等教育发展和进步为导向，依托自主研发的高等教育评价专利技术和“大学360度数据监测平台”的大数据支持，采用数百项指标变量对中国大学进行全方位、体系化、监测式评价，向学生、家长和全社会提供及时、可靠、丰富的高校可比信息（查看排名方法）。"></u--text>
											</u-row>
											<u-row customStyle="margin-top: 15px">
												<u--image :src="src1"></u--image>
											</u-row>
											<u-row>
												<u-grid :border="false" @click="click">
													<u-grid-item v-for="(baseListItem,baseListIndex) in list2" :key="baseListIndex">
														<u-icon
															:customStyle="{paddingTop:40+'rpx'}"
															:name="baseListItem.name"
															:size="22"
														></u-icon>
														<text class="grid-num">{{baseListItem.num}}</text>
													</u-grid-item>
												</u-grid>
												<u-toast ref="uToast" />
											</u-row>
										</view>
									</li>
								</ul>
							</u-row>
                        </u-col>
                        <u-col span="4">
                        	
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
				src1: 'https://cdn.uviewui.com/uview/album/1.jpg',
				keyword: '',
				baseList: [
					{
						title: '资讯',
						url: '../index/index'
					},
					{
						title: '社区',
						url: '../community/community'
					},
					{
						title: '探索',
						url: ''
					},
				],
				list1: [
					{
						name: '关注',
					}, 
					{
				        name: '推荐',
				    },
					{
					    name: '图文',
					},
					{
					    name: '视频',
					}
				],
				list2: [
					{
						name: 'thumb-up',
						num: '2312'
					},
					{
						name: 'chat',
						num: '424'
					},
					{
						name: 'star',
						num: '431'
					}
				]
			}
		},
		onLoad() {
			this.loadmore()
		},
		methods: {
			click(url) {
				uni.navigateTo({
					url: url
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
			}
		}
	}
</script>


<style lang="scss">
	*{
		margin: 0;
		padding: 0;
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
	
	.grid-num {
		font-size: 15px;
		color: #909399;
		padding: 0px 20px 0px 20px;
		/* #ifndef APP-PLUS */
		box-sizing: border-box;
		/* #endif */
	}
</style>