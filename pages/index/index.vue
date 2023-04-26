<template>
	<view class="root">
		<!-- 展示部分 -->
		<view class="show-item">
			<view class="show-item-top">
			<!-- 	<view class="show-box">
					{{num5}}
				</view> -->
			</view>
			<view class="show-item-bottom">
				{{num1}}
			</view>
		</view>
		<!-- 操作部分 -->
		<view class="operate">
			<view class="operate-box">
				<view class="operate-item1" @click="clear">
					C
				</view>
				<view class="operate-item2" @click="fu">
					<image src="../../static/youtian-calc/zf.png" mode=""></image>
				</view>
				<view class="operate-item2" @click="ys('%')">
					<image src="../../static/youtian-calc/bfh.png" mode=""></image>
				</view>
				<view class="operate-item3" @click="ys('/')">
					<image src="../../static/youtian-calc/chu.png" mode=""></image>
				</view>
			</view>
			<view class="operate-box">
				<view class="operate-item4" @click="number('7')">
					<image src="../../static/youtian-calc/7.png" mode=""></image>
				</view>
				<view class="operate-item4" @click="number('8')">
					<image src="../../static/youtian-calc/8.png" mode=""></image>
				</view>
				<view class="operate-item4" @click="number('9')">
					<image src="../../static/youtian-calc/9.png" mode=""></image>
				</view>
				<view class="operate-item3" @click="ys('*')">
					<image src="../../static/youtian-calc/cheng.png" mode=""></image>
				</view>
			</view>
			<view class="operate-box">
				<view class="operate-item4" @click="number('4')">
					<image src="../../static/youtian-calc/4.png" mode=""></image>
				</view>
				<view class="operate-item4" @click="number('5')">
					<image src="../../static/youtian-calc/5.png" mode=""></image>
				</view>
				<view class="operate-item4" @click="number('6')">
					<image src="../../static/youtian-calc/6.png" mode=""></image>
				</view>
				<view class="operate-item3" @click="ys('-')">
					<image src="../../static/youtian-calc/jian.png" mode=""></image>
				</view>
			</view>
			<view class="operate-box">
				<view class="operate-item4" @click="number('1')">
					<image src="../../static/youtian-calc/1.png" mode=""></image>
				</view>
				<view class="operate-item4" @click="number('2')">
					<image src="../../static/youtian-calc/2.png" mode=""></image>
				</view>
				<view class="operate-item4" @click="number('3')">
					<image src="../../static/youtian-calc/3.png" mode=""></image>
				</view>
				<view class="operate-item3" @click="ys('+')">
					<image src="../../static/youtian-calc/jia.png" mode=""></image>
				</view>
			</view>
			<view class="operate-box">
				<view class="operate-item5" @click="number('0')">
					<view class="operate-item4">
						<image src="../../static/youtian-calc/0.png" mode=""></image>
					</view>
				</view>
				<view class="operate-item4" @click="number('.')">
					<image src="../../static/youtian-calc/dian.png" mode=""></image>
				</view>
				<view class="operate-item3" @click="ys('=')">
					<image src="../../static/youtian-calc/dengyu.png" mode=""></image>
				</view>
			</view>
		</view>

	</view>
</template>

<script>
	export default {
		data() {
			return {
				num1: 0, //显示的操作数
				num2: 0, 
				num3: 0, 
				num4: 0, 
				num5: '',//操作符 
				isOne: true,//是否第一次
                isTwo: true,//是否第二次输入操作符
                isshow:true//是否显示
			}
		},
		methods: {
			// 清除操作
			clear() {
				console.log('clear')
				this.num1 = 0
				this.num5 = ''
				this.isOne = true
			},
            fu(){
                this.num1=-this.num1
            },
			// 进行运算
			ys(e) {
                //将用户第一次输入的值赋值给num2,记录运算符
                if(this.isTwo){
                     this.cz()
                     this.num2=this.num1
                     this.num5=e 
                     this.isshow=true
                }    
                this.isOne=false 
			},
            cz(){
                if(this.num5=="+"){
                     this.num1=Number(this.num2)+Number(this.num1)
                  }else if(this.num5=="-"){
                      this.num1=Number(this.num2)-Number(this.num1)
                  }else if(this.num5=="*"){
                      this.num1=Number(this.num2)*Number(this.num1)
                  }else if(this.num5=="/"){
                      this.num1=Number(this.num2)/Number(this.num1)
                  }else if(this.num5=="%"){
                      this.num1=Number(this.num2)%Number(this.num1)
                  }
                      this.num2=0
            },
			// 点击的数字
			number(e) {
                // if(this.num1==0){
                //     this.num1=e;
                //     return
                // }
                //判断是否第一次输入
                if(this.isOne){
                   if (this.num1!=0) {
						this.num1 += e
					} else {
						this.num1 = e
					}   
                }else{
                    if(this.isshow){
                        if(this.num1<0){
                           this.num1=-e 
                        }else{
                           this.num1=e 
                        }
                         this.isshow=false
                    }else{
                        this.num1 += e
                    }
                  
                }
                 
			}
		}
	}
</script>

<style lang="scss" scoped>
	.root {
		background: black;
	}

	.show-item {
		height: 33vh;
		width: 100%;

		.show-item-top {
			height: 66%;
			width: 95%;
			position: relative;

			.show-box {
				height: 20%;
				width: 100%;
				position: absolute;
				bottom: 0;
				font-size: 50rpx;
				text-align: right;
				color: white;
			}
		}

		.show-item-bottom {
			height: 33%;
			width: 95%;
			color: white;
			font-size: 120rpx;
			text-align: right;
		}
	}

	.operate {
		height: 60vh;
		width: 100%;

		.operate-box {

			display: flex;
			justify-content: center;
			margin-bottom: 20rpx;

			.operate-item1 {
				width: 160rpx;
				height: 160rpx;
				background: rgb(165, 165, 165);
				border-radius: 50%;
				margin: 0 10rpx;
				color: #2c2c2c;
				font-size: 70rpx;
				text-align: center;
				line-height: 160rpx;
			}

			.operate-item2 {
				width: 160rpx;
				height: 160rpx;
				background: rgb(165, 165, 165);
				border-radius: 50%;
				margin: 0 10rpx;
				text-align: center;

				image {
					height: 70rpx;
					width: 70rpx;
					margin-top: 45rpx;
				}
			}

			.operate-item3 {
				width: 160rpx;
				height: 160rpx;
				background: rgb(254, 160, 12);
				border-radius: 50%;
				margin: 0 10rpx;
				text-align: center;

				image {
					height: 70rpx;
					width: 70rpx;
					margin-top: 45rpx;
				}
			}

			.operate-item4 {
				width: 160rpx;
				height: 160rpx;
				background: rgb(51, 51, 51);
				border-radius: 50%;
				margin: 0 10rpx;
				text-align: center;

				image {
					height: 70rpx;
					width: 70rpx;
					margin-top: 45rpx;
				}
			}

			.operate-item5 {
				width: 330rpx;
				height: 160rpx;
				background: rgb(51, 51, 51);
				border-radius: 90rpx;
				margin: 0 10rpx;
				text-align: center;

				image {
					height: 70rpx;
					width: 70rpx;
					margin-top: 45rpx;
				}
			}

			.operate-item {
				width: 160rpx;
				height: 160rpx;
				background: rgb(165, 165, 165);
				border-radius: 50%;
				margin: 0 10rpx;
			}
		}
	}
</style>