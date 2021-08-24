<template>
	<view v-if="data">
		<uni-notice-bar style="margin: 0;" single :text="msg" showIcon :speed="50" scrollable></uni-notice-bar>
		<uni-swiper-dot :info="carouselItems" field="title" :current="current" mode="nav">
			<swiper @change="swiperChange" :indicator-dots="false" :autoplay="true" :interval="3000" :duration="1000">
				<swiper-item class="swipe" v-for="(item, index) in carouselItems" @click="goDetail(item.title,item.href)"><image :src="baseUrl + item.img" mode=""></image></swiper-item>
			</swiper>
		</uni-swiper-dot>
		<view v-for="(value,key) in items" :key="key">
			
		
			<view class="advice" >
				<uni-icons size="20" type="shop"></uni-icons>
				<text>{{value.title}}</text>
			</view>
			<view class="grid">
				<uni-grid :column="2" :showBorder="false"  :square="false" :highlight="false" >
				    <uni-grid-item v-for="(item,index) in value.data" :key="index">
				        <view class="item_card">
				        	<image :src="baseUrl+item.pic" mode=""></image>
							<view>
								<view>{{item.title}}</view>
								<view>{{item.details}}</view>
								<view>{{item.price}}</view>
								<button type="primary" size="mini">查看详情</button>
							</view>
				        </view>
				    </uni-grid-item>
				    
				</uni-grid>
			</view>
			
		</view>
	
	</view>
</template>

<script>
export default {
	data() {
		return {
			msg:'热烈庆祝 学子商城App 成功制作, 希望同学们能够独立完成此作品!',
			baseUrl:'http://101.96.128.94:9999/',
			data:null,
			current: 0,
			
			       
		}
	},
	methods: {
		goDetail(title,href){
			console.log(title,href);
			uni.navigateTo({
				url: `/pages/detail/detail?href=${href}&title=${title}`,
				
			});
		},
		getData(){
			const url='http://101.96.128.94:9999/data/product/index.php'
			uni.request({
				url,
				method: 'GET',
				data: {},
				success: res => {
					console.log(res);
					this.data=res.data;


				},
				fail: (err) => {
					console.log(err);
				},
				complete: () => {}
			});
		},
		swiperChange(e){
			this.current=e.detail.current;
			
		}
	},
	mounted() {
		this.getData();
		

	},
	computed:{
		carouselItems() {
					return this.data.carouselItems;
				},
		items() {
					return [
						{ title: '1F/首页推荐', data: this.data.recommendedItems },
						{ title: '2F/热销单品', data: this.data.topSaleItems},
						{ title: '3F/最新上架', data: this.data.newArrivalItems}
					];
				}
	}
}
</script>

<style lang="scss">
.swipe {
	> image {
		width: 750rpx;
		height: 322rpx;
	}
}
.advice{
	font-size: 1.1em;
	width: 100%;
	height: 80rpx;
	font-weight: bold;
	line-height: 80rpx;
	background-color: rgb(241,243,242);
	>text{
		margin-left: 20rpx;
	}	
}
.grid{
	padding: 6rpx;
	
}
.item_card{
	margin: 6rpx;
	border: 1px solid gray;
	border-radius: 5rpx;
	
	>image{
		width: 100%;
		height: 250rpx;
	}
	>view{
		padding: 10rpx;
		view{
			text-overflow: ellipsis;
			white-space: nowrap;
			overflow: hidden;
			&:first-child{
				font-weight: bold;
			}
			&:nth-child(2){
				font-size: 0.8em;
				color: gray;
				margin: 4rpx 0;				
			}
			&:nth-child(3){
				 color: red;
				font-size: 1.1em;
			}
		}
	}
}
</style>
