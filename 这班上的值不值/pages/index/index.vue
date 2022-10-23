<template>
	<div>
		<view class="content">
			<div style="margin-top: 16px; font-size: 16px; color: #c4c9ca; text-align: center;">
				算算你的工作值不值

			</div>
			<div style="margin-top: 6px; font-size: 16px; color: #c4c9ca; text-align: center;">算法来源：知乎 @拉拉拍皮球</div>

			<div v-show="show">
				<div class="input-box">
					<h3>平均日薪（必填）</h3>
					<input placeholder-style="color:#cacaca;" placeholder="月薪/工作日" v-model="inputs.day_wage"
						maxlength="5" type="number">
				</div>
				<div class="input-box">
					<h3>工作时长（必填）</h3>
					<input placeholder-style="color:#cacaca;" placeholder="上班时间-下班时间" v-model="inputs.work_time"
						maxlength="5" type="number">
				</div>
				<div class="input-box">
					<h3>通勤时长（必填）</h3>
					<input placeholder-style="color:#cacaca;" placeholder="上下班在路上的时间单位小时" v-model="inputs.journey_time"
						maxlength="5" type="number">
				</div>
				<div class="input-box">
					<h3>每天摸鱼时长（必填）</h3>
					<input placeholder-style="color:#cacaca;" placeholder="不干活+吃饭+午休时间" v-model="inputs.touch_fish"
						maxlength="5" type="number">
				</div>
				<h3 style="font-size: 12px; color:#ff3612;margin-top:6px;">
					{{info}}
				</h3>
				<div @click="nuxt" class="next">下一步</div>
			</div>

			<div v-show="!show">
				<div class="input-box">
					<h3>选择学历（必填）</h3>
					<select @change="factors" v-model="selects.edu_how">
						<option value="0">你的学历如何？</option>

						<option value="0.8">专科及一下</option>

						<option value="1">普通本科</option>

						<option value="1.2">高级本科</option>

						<option value="1.4">普通硕士</option>

						<option value="1.6">高级硕士</option>

						<option value="1.8">普通博士</option>

						<option value="2.0">高级博士</option>
					</select>
				</div>
				<div class="input-box">
					<h3>选择工作环境（必填）</h3>
					<select @change="factors" v-model="selects.environment">
						<option value="0">工作环境如何？</option>

						<option value="0.8">郊区工厂/工地/等艰苦环境</option>

						<option value="0.9">工厂/工地/户外等工作环境</option>

						<option value="1">办公室等常规环境</option>

						<option value="1.1">CBD/体制内等工作环境</option>
					</select>
				</div>
				<div class="input-box">
					<h3>同事颜值（必填）</h3>
					<select @change="factors" v-model="selects.beautiful">
						<option value="0">同事的颜值如何？</option>

						<option value="0.9">没有帅哥（美女）</option>

						<option value="1">不多不少</option>

						<option value="1.1">美女（帅哥）很多</option>
					</select>
				</div>
				<div class="input-box">
					<h3>同事质量（必填）</h3>
					<select @change="factors" v-model="selects.ability">
						<option value="0">同事质量？</option>

						<option value="0.95">SB太多了</option>

						<option value="1">大部分都是正常人</option>

						<option value="1.05">优秀大佬很多</option>
					</select>
				</div>
				<div class="input-box">
					<h3>职业资质需要（必填）</h3>
					<select @change="factors" v-model="selects.qualification">
						<option value="0">职业需不需要资质？</option>

						<option value="1">无要求、二级</option>

						<option value="1.05">建造造价监理</option>

						<option value="1.1">建筑岩土结构</option>

						<option value="1.15">主任医师、教授</option>
					</select>
				</div>
				<div class="input-box">
					<h3>上班时间（必填）</h3>
					<select @change="factors" v-model="selects.go_work_time">
						<option value="0">你的上班时间？</option>

						<option value="0.95">08:30前上班</option>

						<option value="1">08:30后上班</option>
					</select>
				</div>
				<h3 style="font-size: 12px; color:#ff3612;margin-top:6px;">
					{{info}}
				</h3>
				<div @click="ok" class="next">查看结果</div>
				<div @click="nuxt" class="up">返回上一步</div>
			</div>
		</view>
		<a href="https://mp.weixin.qq.com/mp/profile_ext?action=home&__biz=Mzk0NzM5MzU1MA==&scene=110#wechat_redirect"
			style="display: block; width: 100%; text-align: center; margin-top: 18px; padding-bottom: 30px;">公众号：抓鱼鸭</a>
	</div>
</template>

<script>
	export default {
		data() {
			return {
				title: 'Hello',
				inputs: {
					day_wage: '',
					work_time: '',
					journey_time: '',
					touch_fish: ''
				},
				selects: {
					edu_how: '0',
					environment: '0',
					beautiful: '0',
					ability: '0',
					qualification: '0',
					go_work_time: '0',
					factor: '0'
				},
				show: true,
				info: ''
			}
		},
		onLoad() {

		},
		methods: {
			ok() {
				if (this.selects.edu_how != '0' && this.selects.environment != '0' && this.selects.beautiful != '0' && this
					.selects.ability != '0' && this.selects.qualification != '0' && this.selects.go_work_time != '0') {
					let a = ((parseFloat(this.inputs.day_wage) * parseFloat(this.selects.factor)) / (35 * (parseFloat(this
						.inputs.work_time) + parseFloat(this.inputs.journey_time) - 0.5 * parseFloat(this
						.inputs.touch_fish)) * parseFloat(this.selects.edu_how) * parseFloat(this.selects
						.qualification))) * parseFloat(this.selects.go_work_time)
					
					uni.navigateTo({
						url: '/pages/result/result?res=' + a.toFixed(2),
						fail(err) {
							console.log(err)
				 	}
					});
				} else {
					this.info = '本页面全部必选，选完在查看结果'
				}





			},
			nuxt() {
				if (this.inputs.day_wage != '' && this.inputs.work_time != '' && this.inputs.journey_time != '' && this
					.inputs.touch_fish != '') {
					this.show = !this.show
					this.info = ''
				} else {
					this.info = '本页面全部必填，填完在下一步'
				}

			},

			factors() {
				let b = 1 * parseFloat(this.selects.environment) * parseFloat(this.selects.beautiful) * parseFloat(this
					.selects.ability) //综合环境公式
				this.selects.factor = b.toFixed(1)
				console.log(this.selects.factor)
			},
		}
	}
</script>

<style>
	.content {
		width: 88%;
		margin: 0 auto;
	}




	.input-box {
		width: 100%;
		margin-top: 12px;
	}

	.input-box input {
		width: 100%;
		height: 38px;
		background-color: #f8fcff;
		border: 2px solid #12AAFF;
		border-radius: 10px;
		outline: none;
		box-sizing: border-box;
		padding-left: 12px;
	}

	.input-box h3 {
		font-size: 14px;
		font-weight: 300;
		margin-bottom: 5px;
	}

	.next {
		width: 100%;
		height: 50px;
		background-color: #12AAFF;
		text-align: center;
		line-height: 50px;
		color: #fff;
		margin-top: 28px;
		border-radius: 10px;
	}

	select {
		width: 100%;
		height: 38px;
		background-color: #f8fcff;
		border: 2px solid #12AAFF;
		border-radius: 10px;
		outline: none;
		box-sizing: border-box;
		padding-left: 8px;
	}

	.up {
		width: 100%;
		height: 50px;
		background-color: #f6fcff;
		border: 2px solid #12AAFF;
		text-align: center;
		line-height: 50px;
		color: #12AAFF;
		margin-top: 20px;
		border-radius: 10px;
	}
</style>
placeholder-style="color:#cacaca;"
