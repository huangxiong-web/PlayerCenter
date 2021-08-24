<template>
	<view style="display: flex;">
		<scroll-view 
		scroll-y="true" 
		class="scroll_y"
		:style="{height:windowHeight+'px'}">
			<view 
			class="menucell" 
			:class="{cur: current == index}" 
			hover-class="active"
			v-for="(item,index) in hero" 
			:key="index"
			@click="doCheckMenu(index)">
				{{item.title}}
			</view>
		</scroll-view>
		<scroll-view 
		v-if="data && showRight"
		scroll-y="true"  
		style="width: 70%; background-color: #eee;"
		:style="{height:windowHeight+'px'}">
			<view class="hero_intr">
				<view class="header">
					<image :src="heroIcon" mode=""></image>
					<view>
						<view>{{heroInfo.title}}</view>
						<view>昵称：{{heroInfo.name}}</view>
						<view>金币：{{heroInfo.goldPrice}}</view>
						<view>点券：{{heroInfo.couponPrice}}</view>
					</view>
				</view>
				<uni-card title="背景故事" isFull>
					<view style="font-size: 0.9em;">
						{{ heroInfo.shortBio }}
					</view>
				</uni-card>
				<uni-collapse>
					<uni-collapse-item title="使用建议">
						<uni-list>
							<uni-list-item v-for="(item,index) in heroInfo.allytips" :title="item" :key="index">
							</uni-list-item>
						</uni-list>
					</uni-collapse-item>
				
					
						<uni-collapse-item title="对战技巧">
							<uni-list>
								<uni-list-item v-for="(item,index) in heroInfo.enemytips" :title="item" :key="index">
									
								</uni-list-item>
							</uni-list>
						</uni-collapse-item>
					
					
						<uni-collapse-item title="技能说明">
							<uni-list>
								<uni-list-item v-for="(item,index) in spells" :key="index" 
								:thumb="item.abilityIconPath" 
								:title="item.name"
								 thumbSize="lg"
								 :note="item.description"
								 direction="column">
									
								</uni-list-item>
							</uni-list>
						</uni-collapse-item>
						<uni-collapse-item title="皮肤">
							<uni-list>
								<uni-list-item v-for="(item,index) in skins" :key="index" :title="item.name" :note="item.description" :thumb="item.iconImg" thumbSize="lg"></uni-list-item>
								
							</uni-list>
						</uni-collapse-item>
					</uni-collapse>	
					
				
			</view>
		</scroll-view>
	</view>
</template>

<script>
export default {
	data() {
		return {
			hero:[],
			current:0,
			data:null,
			showRight:true,
		};
	},
	methods: {
		getData(){
			const url='https://game.gtimg.cn/images/lol/act/img/js/heroList/hero_list.js?v=50'
			uni.request({
				url,
				method: 'GET',
				data: {},
				success: res => {
					console.log(res);
					this.hero=res.data.hero;
					const heroId=res.data.hero[0].heroId;
					this.getHeroDetail(heroId);
				},
				fail: (err) => {
					console.log(err);
				},
				complete: () => {}
			});
		},
		getHeroDetail(heroId){
			const url=`https://game.gtimg.cn/images/lol/act/img/js/hero/${heroId}.js`;
			uni.request({
				url,
				method: 'GET',
				data: {},
				success: res => {
					console.log(res);
					this.data=res.data;
					this.showRight = false;
					this.$nextTick(()=>{
						this.showRight = true;
					})	
														
				},
				fail: (err) => {
					console.log(err);
					
					
				},
				complete: () => {}
			});
			
		},
		doCheckMenu(index){
			this.current=index;
			const heroId=this.hero[index].heroId;
			this.getHeroDetail(heroId);
		}
	},
	mounted() {
		this.getData();
	},
	computed:{
		windowHeight(){
			return uni.getSystemInfoSync().windowHeight;
					},
		heroInfo(){
			return this.data.hero;
		},
		skins(){
			return this.data.skins;
		},
		spells(){
			return this.data.spells;
		},
		heroIcon() {
			return `https://game.gtimg.cn/images/lol/act/img/champion/${this.heroInfo.alias}.png`;		
				}
	}
};
</script>

<style lang="scss">
	.scroll_y{
		height: 100%;
		width: 30%;
		display: flex;
	}
	.menucell{
		width: 100%;
		height: 80rpx;
		text-align: center;
		line-height: 80rpx;
		background-color: white;	
		border-bottom: 1px solid rgb(211,211,211);
	}
	.cur{
		background-color:#eee;
		color:rgb(23,147,198);
	}
	.active{
		
	}
	
	.header{
		display: flex;
		>image{
			width: 180rpx;
			height: 180rpx;
		}
		>view{
			padding: 10rpx;
			view:first-child{
				font-size: 1.2em;
				font-weight: bold;
			}
		}
		
	}
</style>
