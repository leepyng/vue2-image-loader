# vue2-image-loader
a image loader component for vue2
<p align="center">


<img src="https://github.com/leepyng/vue2-image-loader/blob/master/git/QQ20180723-182926.gif" alt="Coverage Status">


</p>

# install

	
	npm install vue2-image-loader --save-dev
	

# how to use
	template:
		<ImgLoader :defaultImgUrl="'error.png'" :imgUrl="imgurl" />
	
	script:
		//import
		import ImgLoader from 'vue2-image-loader'
		//define
		components:{
			ImgLoader
		}
		
	
# props description
	defaultImgUrl:a default image if the target image can't load
	imgUrl:target image to load
