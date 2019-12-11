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
			<view-list :imgList = "imgList"></view-list>
		</view>
	</view>
</template>

<script>
	import ViewList from './../components/view-list/view-list'
	export default {
		data() {
			return {
				picType:'1',
				currentIndex: 0,
				imgList :[],
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
						name:'自拍',
						type:'11'
					},{
						name:'街拍',
						type:'11'
					},{
						name:'每日',
						type:'11'
					}
				]
			};
		},
		onLoad(){
			this.getList();
		},
		onPullDownRefresh() {
			//监听下拉刷新动作的执行方法，每次手动下拉刷新都会执行一次
			this.getList()
		},
		methods: {
			getImageType(type,index){
				if(this.currentIndex!=index){
					this.picType = type;
					this.currentIndex = index;
					this.getList();
				}
			},
			getList(){
				console.log(this.picType);
				let _self = this;
				uni.request({
				    url: 'http://106.12.26.79:1000/getimg', //仅为示例，并非真实接口地址。
				    data: {
				        // text: 'uni.request'
						pageSize:12,
						pageNum:1,
						cagetory: _self.picType
				    },
				    header: {
				        
				    },
				    success: (res) => {
						console.log(res)
						if(res.data.msg === 'success') {
							_self.imgList = res.data.data.page;
							uni.stopPullDownRefresh();
						}
				    }
				});
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
