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
						    <u-grid :border="false" @click="click">
						        <u-grid-item v-for="(baseListItem,baseListIndex) in baseList" :key="baseListIndex">
						            <text>{{baseListItem.title}}</text>
						        </u-grid-item>
						    </u-grid>
						    <u-toast ref="uToast" />
						</u-col>
						<u-col span="3" offset="1">
						    <u-search placeholder="请输入搜索内容" v-model="keyword"></u-search>
						</u-col>
						<u-col span="0.2" offset="1.5">
							<u-avatar :src="src"></u-avatar>
						</u-col>
						<u-col span="2.8">
							<u--text text="EasyKnow" size="10px"></u--text>
						</u-col>
                    </u-row>
					<view style="width: 66%; float: left;">
						<u-row customStyle="margin-bottom: 10px"  justify="flex-start">
							<u-col span="10" offset="2">
								<h2 style="text-align: center; margin-top: 20px;"></h2>
								<view class="article">
									<unicloud-db v-slot:default="{data, loading, error, options}" :options="formData" collection="opendb-news-articles" :where="where" :field="field"
									 :getone="true"  :manual="true" ref="detail" @load="loadData">
										<template v-if="!loading && data">
											<view class="article-title">{{title}}</view>
											<!-- <uni-list :border="false">
												<uni-list-item thumbSize="lg" :thumb="data.author_avatar">
													<template v-slot:body>
														<view class="header-content">
															<view class="uni-title">{{data.author_name}}</view>
															<view class="uni-note">更新于 {{data.last_modify_date}} </view>
														</view>
													</template>
													<template v-slot:footer>
														<view class="footer">
															<button class="footer-button">关注</button>
														</view>
													</template>
												</uni-list-item>
											</uni-list> -->
											
												<!-- 文章开头，缩略图 -->
												<!-- <image class="banner-img" :src="data.cover" mode="widthFix"></image> -->
												<!-- 文章摘要 -->
												<view class="banner-title">
													<text class="uni-ellipsis">{{data.excerpt}}</text>
												</view>
											
											<view class="article-content">
												<rich-text :nodes="data.content" style="font-size: 14px;line-height: 1.8;"></rich-text>
											</view>
										</template>
									</unicloud-db>
								</view>
									<!-- <u--text text="内地升学四大途径
						港澳台学生到内地升学主要可分为四大类：1) 港澳台联合招生考试；2) 两校联招考试；3) 免试招生；4) 全英语授课本科课程。对有意到内地升学的港澳台学生来说，港澳台联合招生考试是最主要的途径，可以报考全国约300所大学。录取批次分本科和预科两个批次。本科志愿组考生可填报10个顺序排列的院校志愿，每所院校可填报6个专业志愿和1个专业服从选项，预科志愿组可填报5个顺序排列的院校志愿。
						
						报考港澳台联合招生考试，学生需有高中毕业(完成中六课程)或同等程度。由于考试有独立制定的考核科目以及范围，为了考取更好的成绩，很多港澳台学生都会报读一年制的港澳台联招预备班。中国留学社根据会员提供的资讯，在讨论区内列出了在香港及内地开办的港澳台联招预备班名单，教得比较好的机构不要太晚才去报名，因为名额有限，很多学生都会提早报名。有关详情，请到-港澳台联招考试。
						两校联招考试
						申请暨南大学和华侨大学，可以报考两校联招考试(暨南大学、华侨大学联合招生考试)。考试形式和范围与港澳台联招考试并不相同。由于经港澳台联招考试也可报考暨南大学和华侨大学，港澳台考生可同时参加两校联招和全国联招考试。
						
						暨南大学、华侨大学另有免试招收港澳台学生的入学方法。香港中六生可以用香港中学文凭考试成绩申请，副学士和高级文凭学生达到成绩要求，可免予笔试，择优录取入本科各专业或预科班。台湾学生可以用学科能力测试成绩或大学指定科目考试申请，择优录取入本科各专业或预科班。有关详情，请到-暨南大学入学途径
						免试招生
						香港学生：新高中学制的香港学生除了参加港澳台联招考试外，也可以依据2022年香港中学文凭考试(HKDSE) 成绩报考129所内地高等院校。有关详情，请到-内地高校招收香港中学文凭考试学生计划。
						
						除免试招收香港学生计划之外，中山大学可以单独招收香港学生，考生可以报考中山大学的独立招生考试(自2021年起暂停)。
						
						台湾学生：内地大学可依据台湾学科能力测验成绩招收台湾高中毕业生。有关详情，请到-学科能力测验成绩招收台湾学生
						全英语授课本科课程
						内地升学的另外一个途径是选择入读中外合作大学，这类型的大学凭借着英语教学环境和国际化等优势，吸引内地优秀学生和来自全球多个国家和地区的学生入读。港澳台学生申请可以不经过港澳台联招考试和免试招收香港及台湾学生的方法，有关详情，请到-英语授课课程
						设计及艺术类
						内地大学当中，有以美术为主，达到世界级水平的美术高等学院。由于美术高等学院专门为有志于设计及艺术类升学的学生而设，因此设计类专业选择也比较多及全面。有关设计及艺术类的资料请到-设计及艺术类
						
						如果大家想更深入了解港澳台学生到内地升学的各种途径，在内地大学就读港澳台学生的经验，有意到内地升学的2022、2023届港澳台学生请到讨论区浏览最新考试资讯和认识其他在内地升学的港澳台学生，有关资料请到-中国留学社讨论区"></u--text>
								 -->
							</u-col>
						</u-row>
					</view>
					<view style="width: 33%; float: left;">
						<u-row customStyle="margin-top: 50px">
							<u-col span="1" offset="4">
								<u-avatar :src="src" size="60"></u-avatar>
							</u-col>
							<u-col span="11" offset="0.5">
								<u--text text="EasyKnow" size="20px"></u--text>
							</u-col>
						</u-row>
						<u-row>
							<u-col span="6" offset="3.5">
								<u-grid :border="false" @click="click">
									<u-grid-item v-for="(listItem,listIndex) in list" :key="listIndex">
										<text class="grid-text">{{listItem.title}}</text>
										<text class="grid-num">{{listItem.num}}</text>
									</u-grid-item>
								</u-grid>
								<u-toast ref="uToast" />
							</u-col>
						</u-row>
						<u-row>
							<u-col span="6" offset="3.7">
								<u-row>
									<u-text text="常用关键词:"></u-text>
								</u-row>
								<u-row customStyle="margin-top: 10px">
									<text>
										<text class="word" v-for="(item, index) in wordList" :key="index">{{item}}</text>
									</text>
								</u-row>
							</u-col>
						</u-row>
						<u-row>
							<u-col span="6" offset="3.7">
								<u-row customStyle="margin-top: 20px">
									<u-text text="个人介绍:"></u-text>
								</u-row>
								<u-row  customStyle="margin-top: 10px">
									<u--text :lines="1" text="对港澳同胞在内地的升学政策非常了解，已有多篇文章获得高赞"></u--text>
								</u-row>
							</u-col>
						</u-row>
					</view>
                </view>
            </view>
        </view>
</template>

<script>
	import htmlParser from '@/common/html-parser'
	export default {
		data() {
			return {
				id:"626957cdeb9d4c00017aeeaf",
				title:'',
				// 查询字段，多个字段用 , 分割
				field: 'title,author_avatar,author_name,author_name,last_modify_date,cover,excerpt,content',
				formData: {
					noData: '<p style="text-align:center;color:#666">详情加载中...</p>'
				}, 
				src: '/static/logo.png',
				keyword: '',
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
				list: [
					{
						title: '作品',
						num: 10
					},
					{
						title: '粉丝',
						num: 198
					},
					{
						title: '获赞',
						num: 435
					},
				],
				wordList: ['作品', '粉丝', '获赞', '获赞','获赞','获赞','获赞']
			}
		},
		computed:{
			//拼接where条件
			//查询条件 ,更多详见 ：https://uniapp.dcloud.net.cn/uniCloud/uni-clientDB?id=jsquery
			where(){
				console.log(this.id);
				return `_id =="${this.id}"`
			}
		},
		onLoad(event) {
			//获取真实新闻id，通常 id 来自上一个页面
			if(event.id){
				this.id = event.id
			}
			//若上一页传递了标题过来，则设置导航栏标题
			if(event.title){
				this.title = event.title
				uni.setNavigationBarTitle({
					title:event.title
				})
			}
			this.loadmore()
		},
		onReady() {
			// 开始加载数据，修改 where 条件后才开始去加载 clinetDB 的数据 ，需要等组件渲染完毕后才开始执行 loadData，所以不能再 onLoad 中执行
			if(this.id){// ID 不为空，则发起查询
				this.$refs.detail.loadData()
			}else{
				uni.showToast({
					icon:'none',
					title:'出错了，新闻ID为空'
				})
			}
		},
		methods: {
			click() {
				
			},
			click(name) {
			    this.$refs.uToast.success(`点击了第${name}个`)
			},
			loadData(data){
				console.log(data);
				//如果上一页未传递标题过来（如搜索直达详情），则从新闻详情中读取标题
				if(this.title == '' && data.title){
					this.title = data.title
					uni.setNavigationBarTitle({
						title:data.title
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
	
	.grid-text {
		font-size: 20px;
		color: #909399;
		padding: 10px 20px 10px 0px;
		/* #ifndef APP-PLUS */
		box-sizing: border-box;
		/* #endif */
	}
	
	.grid-num {
		font-size: 15px;
		color: #909399;
		padding: 0px 40px 20px 20px;
		/* #ifndef APP-PLUS */
		box-sizing: border-box;
		/* #endif */
	}
	
	.word {
		font-size: 15px;
		color: #909399;
		padding: 0px 20px 20px 0px;
	}
	.header-content {
		flex: 1;
		display: flex;
		flex-direction: column;
		font-size: 14px;
	}
	
	/* 标题 */
	.uni-title {
		display: flex;
		margin-bottom: 5px;
		font-size: 14px;
		font-weight: bold;
		color: #3b4144;
	}
	
	/* 描述 额外文本 */
	.uni-note {
		color: #999;
		font-size: 12px;
	}
	
	.footer {
		display: flex;
		align-items: center;
	}
	
	.footer-button {
		display: flex;
		align-items: center;
		font-size: 12px;
		height: 30px;
		color: #fff;
		background-color: #ff5a5f;
	}
	
	.banner {
		position: relative;
		margin: 0 15px;
		height: 180px;
		overflow: hidden;
	}
	
	.banner-img {
		position: absolute;
		width: 100%;
	}
	
	.banner-title {
		display: flex;
		align-items: center;
		position: absolute;
		padding: 0 15px;
		width: 100%;
		bottom: 0;
		height: 30px;
		font-size: 14px;
		color: #fff;
		background: rgba(0, 0, 0, 0.4);
		overflow: hidden;
		box-sizing: border-box;
	}
	
	.uni-ellipsis {
		overflow: hidden;
		white-space: nowrap;
		text-overflow: ellipsis;
	}
	
	.article-title {
		padding: 20px 15px;
		padding-bottom: 0;
		font-size: 20px;
		font-weight: 1000;
	}
	
	.article-content {
		padding: 15px;
		font-size: 15px;
		overflow: hidden;
	}

</style>