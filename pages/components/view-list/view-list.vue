<template>
	<view>
		<view class="img-item" v-for="(item,index) in imgList" :key="index">
			<view class="img-content" @click="handleRoute(item._id)">
				<image :src="item.breviary" mode="aspectFit"></image>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		props:{
			imgList:{
				type: Array,
				default:() => []
			}
		
		},
		data() {
			return {
				
			}
		},
		mounted(){
			console.log(this.imgList)
		},
		created(){
			console.log(this.imgList)
		},
		computed:{
		},
		
		methods: {
			handleRoute(id){
				uni.navigateTo({
				    url: '../preview/preview?id='+id
				})
			}
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
