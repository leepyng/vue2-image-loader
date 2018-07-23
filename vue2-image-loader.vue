<template>
	<div v-if="!url">
		<div class="img-loading">
		        <span></span>
		        <span></span>
		        <span></span>
		        <span></span>
		        <span></span>
		</div>
	</div>
	<div v-else-if="url" >
		<img :src="url" />
	</div>
</template>
<script>
	export default{
		name:'img-loader',
		props:{
			imgUrl:{
				type:String,
				default:''
			},
			defaultImgUrl:{
				type:String,
				default:''
			}
		},
		data(){
			return{
				url:''
			}
		},
		watch:{
			imgUrl(){
				this.initData();
			}
		},
		methods:{
			initData(){
				var that=this;
				that.loadImg(that.imgUrl).then((img)=>{
					that.url=img.src;
				}).catch(()=>{
					that.url=that.defaultImgUrl;
				})

			},
			loadImg(image){
				if(!image||image==undefined){
					return Promise.reject();
				}else if (typeof image === 'string') {
					const src = image;
					image = new Image();
					image.src = src;
				}

				const promise = new Promise((resolve, reject) => {
					if (image.naturalWidth) {
						resolve(image);
					} else if (image.complete) {
						reject(image);
					} else {
						image.addEventListener('load', fullfill);
						image.addEventListener('error', fullfill);
					}
					function fullfill() {
						if (image.naturalWidth) {
							resolve(image);
						} else {
							reject(image);
						}
						image.removeEventListener('load', fullfill);
						image.removeEventListener('error', fullfill);
					}
				});
				promise.image = image;
				return promise;
			}
		},
		mounted(){
			this.initData();
		}
	}
</script>
<style scoped>
	.img-loading{
        width: 100%;
        height: .5rem;
        margin: 0 auto;
        position: absolute;
        top: 50%;
        margin-top: -.25rem
    }
    .img-loading span{
        display: inline-block;
        width: 8px;
        height: 50%;
        border-radius: 4px;
        background: lightgreen;
        -webkit-animation: load 1s ease infinite;
    }
    @-webkit-keyframes load{
        0%,100%{
            height: 40px;
            background: lightgreen;
        }
        50%{
            height: 70px;
            margin: -15px 0;
            background: lightblue;
        }
    }
    @-o-keyframes load{
        0%,100%{
            height: 40px;
            background: lightgreen;
        }
        50%{
            height: 70px;
            margin: -15px 0;
            background: lightblue;
        }
    }
    @-ms-keyframes load{
        0%,100%{
            height: 40px;
            background: lightgreen;
        }
        50%{
            height: 70px;
            margin: -15px 0;
            background: lightblue;
        }
    }
    @-moz-keyframes load{
        0%,100%{
            height: 40px;
            background: lightgreen;
        }
        50%{
            height: 70px;
            margin: -15px 0;
            background: lightblue;
        }
    }
    .img-loading span:nth-child(2){
        -webkit-animation-delay:0.2s;
    }
    .img-loading span:nth-child(3){
        -webkit-animation-delay:0.4s;
    }
    .img-loading span:nth-child(4){
        -webkit-animation-delay:0.6s;
    }
    .img-loading span:nth-child(5){
        -webkit-animation-delay:0.8s;
    }

</style>






