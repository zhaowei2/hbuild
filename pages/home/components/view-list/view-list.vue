<template>
	<view>
		<view class="img-list">
			<view class="img-item" v-for="(item,index) in imgList" :key="index">
				<view class="img-content">
					<image :src="item.breviary" mode="aspectFit"></image>
				</view>
			</view>
		</view>
	</view>
</template>

<script>
	import uniLoadMore from './../load-more/load-more/load-more.vue';
	export default {
		props:{
			picType:{
				type:String,
				default:'11'
			}
		
		},
		onLoad: function (options) {
			 setTimeout(function () {
			            console.log('start pulldown');
			        }, 1000);
		 },
		// onPullDownRefresh(success,fail,complete) {
		// 	 console.log('11111111111111')
		// 	 console.log(success)
		// 	 console.log(fail)
		// 	uni.stopPullDownRefresh();
		// },
		data() {
			return {
				imgList:[]
			}
		},
		watch:{
			picType(newdata,olddata){
				if(newdata !== olddata){
					this.getList()
				}
			}
		},
		created() {
			this.getList()
		},
		mounted(){
			console.log('子组件跟新')
		},
		computed:{
		},
		components:{
			uniLoadMore
		},
		methods: {
			getList(){
				console.log(this.picType);
				uni.request({
				    url: 'http://106.12.26.79:1000/getimg', //仅为示例，并非真实接口地址。
				    data: {
				        // text: 'uni.request'
						pageSize:12,
						pageNum:1,
						cagetory: this.picType
				    },
				    header: {
				        
				    },
				    success: (res) => {
						if(res.data.msg === 'success') {
							this.imgList = res.data.data.page;
						}
				    }
				});
			},
			
		}
	}
</script>

<style lang="scss">
.img-item{
	float: left;
	width: 50%;
	.img-content{
		padding: 15upx 0;
		image {
			width: 360upx;
		}
		
	}
}
</style>
