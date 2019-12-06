<template>
	<view>
		<view class="">
		    <scroll-view class="menu-nav" scroll-x="true"  show-scrollbar="false">
				<view :class="['menu-item',currentIndex==index ? 'current-nav':'']" v-for="(item,index) in navList" :key="index" v-on:click="getImageType(item.type,index)">
					{{item.name}}
				</view>
		    </scroll-view>        
		</view>	
		<view class="content">
			<view-list :picType="picType"></view-list>
		</view>
	</view>
</template>

<script>
	import ViewList from './../components/view-list/view-list'
	export default {
		data() {
			return {
				picType:'2',
				currentIndex: 0,
				navList: [
					{
						name:'性感',
						type:'1'
					},{
						name:'日本',
						type:'2'
					},{
						name:'台湾',
						type:'3'
					},{
						name:'清纯',
						type:'4'
					},{
						name:'自拍'
					},{
						name:'街拍'
					},{
						name:'每日'
					}
				]
			};
		},
		methods: {
			getImageType(type,index){
				if(this.currentIndex!=index){
					this.picType = type;
					this.currentIndex = index;
				}
			},
			
		},
		components:{
			ViewList
		}
	}
</script>

<style lang="scss">
.menu-nav {
	overflow: auto hidden;
	width: 100%;
	height: 80upx;
	white-space: nowrap;
	background: #FF73A2 ;
	color: #FFFFFF;
	.menu-item {
		display: inline-block;
		width: 100upx;
		height: 80upx;
		line-height: 80upx;
		text-align: center;
	}
}
</style>
