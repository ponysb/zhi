<template>
	<view style="text-align: center;">
		<div class="box">
			{{one}}
		</div>
		<h3>{{tow}}</h3>
		
		
		<h4>"低于0.8很惨，高于1.5很爽，高于2.0爽到爆"
</h4>
<h5 style="font-size: 14px; color:#d6d6d6; font-weight: 500; margin-top: 12px;">您现在的公司工作状态评分：{{one}}</h5>
<image style="width: 128px; height:128px; margin-top: 150px;" :src="img" mode=""></image>
<a href="https://mp.weixin.qq.com/mp/profile_ext?action=home&__biz=Mzk0NzM5MzU1MA==&scene=110#wechat_redirect" style="display: block; width: 100%; text-align: center; position: absolute; bottom: 60px;">公众号：抓鱼鸭</a>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				one:'0',
				tow:'',
				img:require('../../static/code.png')
			}
		},
		onLoad(option){
		    const res = JSON.parse(decodeURIComponent(option.res));
			console.log(res)
			this.one = res
			if(res.toFixed(2)<0.8){
				this.tow = '太惨了！ 为你抹泪~~'
			}
			
			if(res.toFixed(2)>0.8){
				this.tow = '普普通通！ 马马虎虎！熬着吧。'
			}
			
			if(res.toFixed(2)>1.5){
				this.tow = '好公司啊！ 令人羡慕至极。'
			}
			
			if(res.toFixed(2)>2.0){
				this.tow = '爽爆了！ 大佬您公司还招人吗？'
			}
			
			
		},
		methods: {
			
		}
	}
</script>

<style>
.box{
	width: 150px;
	height: 150px;
	border-radius: 200px;
	background-color: #12AAFF;
	margin: 0 auto;
	margin-top: 50px;
	
	text-align: center;
	color: aliceblue;
	line-height: 150px;
	font-size: 60px;
}
h3{
	font-size: 18px;
	font-weight: 600;
	margin-top: 25px;
	color: #ff3e12;
}
h4{
	font-size: 14px;
	font-weight: 500;
	color: #d6d6d6;
	margin-top: 20px;
}
</style>
