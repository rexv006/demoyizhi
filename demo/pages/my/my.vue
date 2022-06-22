<template>
	<view>
		<!-- 后台按钮组件 -->
		<!-- <zetank-backBar textcolor="#000" :showLeft="true" :showTitle="false" navTitle='标题'></zetank-backBar> -->
		<!-- 用户背景封面 -->
		<z-paging ref="paging" :fixed="true" @scroll="scroll" @query="queryData" :hide-empty-view="true" >
			<image class="info-cover" @tap="fnMainBgPic" src="https://vkceyugu.cdn.bspapp.com/VKCEYUGU-5d36bb3d-8e98-4f00-ab8b-b018dc4f5dc6/17b0292c-8a63-4b7b-a6a6-724f416a9958.jpg"
			  mode="scaleToFill"></image>
			 <!-- 用户头像关注 -->
			 <view class="u-flex-wrap" style="padding-top: 18rpx;padding-bottom: 18rpx;position: relative;align-items: center;display: flex;flex-direction: row;justify-content: flex-end;">
			   <view class="info-avatar">
			     <u-avatar :src="userinfo.avatar" size="135"></u-avatar>
				 
			   </view>
				<view style="margin-right: 50rpx;">
					<u-tag v-if='showedit' text="编辑信息" mode="dark" shape="" bg-color="#f5991e" @click="UserEdit" />
					<view v-if='!showedit' style="height: 45rpx;"></view>
				</view>
			 </view>
			 <!-- 用户名 -->
			  <view style="display: flex;align-items: center;margin-left: 50rpx;margin-top: 20rpx;" v-if="userinfo.length!=0">
			    <text style="font-size: 32rpx;color: #111111;font-weight: bold;margin-right: 10rpx;">{{userinfo.nickname}}</text>
				<u-icon :name="userinfo.gender===1?'man':'woman'" :color="userinfo.gender===1?'#4baed5':'#f5991e'" size="30"></u-icon>
			  </view>
			  
			  <!-- 单位职务 -->
			  <view class="u-flex">
				  <view style="display: flex;align-items: center;margin-left: 50rpx;margin-top: 20rpx;" v-if="userinfo.length!=0">
				      <u-icon name="map-fill" size="32" color="#4baed5"></u-icon>
				      <text style="font-size: 24rpx;color: #555555;margin-left: 10rpx;">{{userinfo.city}}</text>
				    </view>
				  <view style="display: flex;align-items: center;margin-left: 50rpx;margin-top: 20rpx;" v-if="userinfo.length!=0">
				    <u-icon name="man-add-fill" size="32" color="#4baed5"></u-icon>
				    <text style="font-size: 24rpx;color: #555555;margin-left: 10rpx;">{{userinfo.jor}}</text>
				  </view>
			  </view>
			  <!-- 简介-->
			<view style="font-size: 24rpx;color: #555555;margin:20rpx 50rpx;" v-if="userinfo.length!=0">
				<u-tag v-if='membertype!=""' :text="membertype" mode="dark" shape="circle" bg-color="#4baed5" />
				<text style="margin-right: 20rpx;">{{Information==''?'暂无简介':Information}}</text>
			</view>
			<view style="display: flex;align-items: center;margin-left: 50rpx;margin-top: 20rpx;margin-bottom: 20rpx;" v-if="userinfo.length!=0">
			  <text style="font-size: 32rpx;font-weight: bold;color: #555555;margin-right: 18rpx;">{{userinfo.good.length || 0}}</text><text style="font-size: 24rpx;color: gray;margin-right: 28rpx;">粉丝</text>
				<text style="font-size: 32rpx;font-weight: bold;color: #555555;margin-right: 18rpx;">{{userinfo.good.length || 0}}</text><text style="font-size: 24rpx;color: gray;margin-right: 28rpx;">关注</text>
				<text style="font-size: 32rpx;font-weight: bold;color: #555555;margin-right: 18rpx;">{{userinfo.good.length || 0}}</text><text style="font-size: 24rpx;color: gray;margin-right: 28rpx;">点赞</text>
			</view>
			
			<!-- 选择导航 -->
			<view v-if="isFixed" style="height: 90rpx;line-height: 90rpx;background-color: white;margin-bottom: 18rpx;"></view>
			<view id="tabbar" :class="isFixed?'tabbar-fixed':''" style="border-bottom:18rpx #f8f8f8 solid ;align-items: stretch;height: 90rpx;line-height: 90rpx;background-color: white;margin-bottom: 18rpx; display: flex;flex-direction: row;justify-content: space-around;">
			  <view style="font-size: 32rpx;font-weight: bold;text-align: center;width: 128rpx;" :class="current == 0?'tabbarsh':'notabbarsh'" @tap="fnBarClick(0)">导航一</view>
			  <view style="font-size: 32rpx;font-weight: bold;text-align: center;width: 128rpx;" :class="current == 1?'tabbarsh':'notabbarsh'" @tap="fnBarClick(1)">导航二</view>
			</view>
			
			<!-- 导航显示内容 -->
			<view style="margin-top: 2500rpx;">
				
			</view>
		</z-paging>
		
		
	</view>
</template>

<script>
	export default {
		data() {
			return {
				uid:'',
				userinfo:{
					nickname:'zetank',
					avatar:"https://vkceyugu.cdn.bspapp.com/VKCEYUGU-b9e817e6-7ee6-461f-8e66-4bed243cbe98/ad090f5f-2a0f-4ea8-a8b5-fc8dafa4039e.jpg",
					gender:1,
					city:'广州',
					jor:'职务',
					good:{}
				},
				Information:'本人性格热情开朗,待人友好,为人诚实谦虚。工作勤奋,认真负责,能吃苦耐劳,尽职 尽责,有耐心。具有亲和力,平易近人,善于与人沟通',
				membertype:'',
				showedit:true,//信息编辑按钮
				// 是否固定导航
				isFixed: false,
				// 距离顶部达到导航距离
				topNum: 0,
				// 选中 
				current: 0,
				// 导航距离顶部
				tabbarTop: 0,
				clickRefresh: false,
				// 刷新间隔
				timeOutUserInfo: 0,
				// 激活顶部导航关联页状态
				status: {
				  publish: true,
				  praise: false,
				},
			}
		},
		onLoad(option) {
			this.uid = option.uid
			// 等待0.3秒页面渲染,$nextTick使用不能准确
			setTimeout(() => {
			  uni.hideLoading()
			  // 获取导航条距顶部高度
			  this.setTabbarTop();
			}, 300);
			let uid = uni.getStorageSync('uid')
			if(uid === option.uid){
				this.showedit=true
			}
			
			
		},
		methods: {
			// 滚动事件 (需在up配置onScroll:true才生效)
			scroll(e) {
			  this.topNum = e.detail.scrollTop
			  if (e.detail.scrollTop >= this.tabbarTop) {
			    this.isFixed = true // 显示悬浮菜单
			  } else {
			    this.isFixed = false // 隐藏悬浮菜单 
			  }
			},
			// 修改用户背景封面图
			fnMainBgPic() {
				
			},
			//编辑信息
			UserEdit(){
				uni.navigateTo({
					url:""
				})
			},
			/// 顶部导航选项点击
			fnBarClick(current) {
				// console.log(current);
				// 是否当前项点击
				if (this.current == current) {
				  this.timeOutUserInfo += 1;
				  // 是否为刷新值和连续点击2次
				  // console.log('timeOutUserInfo',this.timeOutUserInfo);
				  if (!this.clickRefresh && this.timeOutUserInfo >= 2) {
				    // 刷新值开
					// console.log('点击了两下');
				    this.clickRefresh = true;
				    // 获取新数据
				    
				    // 定时器重置
				    this.timeOutUserInfo = setTimeout(() => {
				      // 清除定时器
					  // console.log('5秒后清除定时器');
				      clearTimeout(this.timeOutUserInfo)
				      // 连续触发记录重置
				      this.timeOutUserInfo = 0;
				      // 5秒后刷新值关
				      this.clickRefresh = false;
				    }, 5000);
				  }
				} else {
				  // 改变顶部导航选中
				  this.current = current;
				  // 首次选中激活顶部导航关联页状态
				  if (!this.status.praise && this.current == 1) this.status.praise = true;
				  // 获取新数据
				  
				  // 清除定时器
				  clearTimeout(this.timeOutUserInfo)
				  // 连续触发记录重置
				  this.timeOutUserInfo = 0;
				  // 刷新值关
				  this.clickRefresh = false;
				}
				// 滚动上滑 
				this.$refs.paging.scrollToY(this.tabbarTop);
				// console.log("滚动上滑");
			},
			// 设置nav到顶部的距离 (滚动条为0, 菜单顶部的数据加载完毕获取到的数值是最精确的)
			setTabbarTop() {
			  let view = uni.createSelectorQuery().in(this).select('#tabbar');
			  view.boundingClientRect(data => {
			    // 到屏幕顶部的距离
			    this.tabbarTop = data.top
			  }).exec();
			},
			queryData(){
				// this.$refs.paging.reload();
				this.$refs.paging.complete([])
			}
		}
	}
</script>

<style>
	.info-cover {
		  display: block;
		  width: 100%;
		  height: 260rpx;
		}
	.info-avatar {
	  position: absolute;
	  left: 0;
	  top: -56rpx;
	  margin-left: 50rpx;
	}
	.tabbarsh {
	  color: #4baed5;
	  border-bottom: 4rpx #4baed5 solid;
	}
	.notabbarsh {
	  color: #555555;
	}
	.tabbar-fixed {
	  position: fixed;
	  left: 0;
	  right: 0;
	  /* #ifdef H5 */
	  top: 0rpx;
	  /* #endif */
	  /* #ifndef H5 */
	  top: 0;
	  /* #endif */
	  z-index: 300;
	  background: #FFFFFF;
	  margin-bottom: 0;
	  border-bottom: 2rpx #EEEEEE solid;
	}
</style>
