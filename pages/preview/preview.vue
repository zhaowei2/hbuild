<template>
	<view>
		<ynGallery 
			 :galleryheight="165" 
			  bkstart="#FFFFFF" 
			  bkend="#FFFFFF" 
			 :imgviewwidth="85" 
			 :imgviewheight="105" 
			 :showbadge="true"
			  badegtype="trian" 
			  badegwidth="25" 
			  badegheight="25" 
			 :showdec="true" 
			 :images="previewList" 
			 >
		</ynGallery>
	</view>
</template>

<script>
	import ynGallery from '../components/YnComponents/ynGallery/ynGallery.vue'
	export default {
		data() {
			return {
				previewList: []
			};
		},
		onLoad(options){
			this.getDetail(options.id)
		},
		components:{
			ynGallery
		},
		methods:{
			getDetail(_id){
				let _self = this;
				uni.request({
					url:'http://106.12.26.79:1000/getimgDetial',
					data:{
						id:_id,
					},
					success: (res) => {
						console.log(res)
						if(res.data.msg === 'success'&&res.data.data.length>0) {
							console.log(res)
							_self.previewList = res.data.data[0].preview;
							console.log(_self)
						}
					}
				})
			}
		}
	}
</script>

<style lang="scss">

</style>
