<template>
<transition name="dialog">
	<div id="dialog-delete" v-if="isShow">
	    <!-- 遮罩 注意top和left -->
		<div id="shade" @click="cancel">
		</div>
	    <!-- 对话框 -->	
		<div id="dialog-delete-box">
			<!-- 	关闭按钮 -->
			<div class="box-top">
			    <span @click="cancel">&times;</span>
			</div>
			<div class="box-content">
			    <p>你确认该球员离队吗?</p>
			    <div class="btn-wrap">
			        <!-- 	确认删除，自定义事件 -->
			        <button class="btn-confirm" @click="confirm">Yes</button>
			        <!-- 	取消删除，自定义事件 -->
			        <button class="btn-cancel" @click="cancel">No</button>
			    </div>
			</div>
		</div>
	</div>
</transition>
</template>

<script>
export default {
	name:"dialog-delete",
	props: {
		isShow: {
			type: Boolean,
			dafault: false
		}
	},
	methods:{
		// 确认删除，自定义事件
		confirm() {
			this.$emit("confirmDel")
		},
		// 取消删除(关闭dialog)，自定义事件
		cancel() {
			this.$emit("cancelDel")
		}			
	}
}
</script>

<style scoped>
/* 遮罩 注意top和left*/
.dialog-enter-active,
.dialog-leave-active {
	transition: all 0.5s;
}
.dialog-enter,
.dialog-leave-to {
	opacity: 0;
}
#shade {
	position: fixed;
	width: 100%;
	height: 100%;
	left: 0;
	top: 0;
	opacity: .5;
	background: #bbb;
	z-index: 99;
}
/* 对话框 注意top和left*/
#dialog-delete-box {
	position: fixed;
	width: 50%;
	 /*最大屏幕高度的50% */  
	max-height: 50%;       
	top: 20%;
	left: 50%;
	overflow: auto;
	/*居中*/
	margin-left: -25%;       
	background: #fefcff;
	z-index:999;
}
.box-top {
	height: 40px;
	margin-bottom: 40px;
}
.box-top span {
	position: absolute;
	right: 0;
	top: 0;
	padding: 0 5px;
	font-size: 22px;
	cursor: pointer;
}
.box-top span:hover {
    background: #306eff;	
}
.box-content {
	text-align: center;
	font-size: 16px;
}
.btn-wrap {
	margin: 50px 0 30px 0;
}
.btn-wrap button {
	padding: 10px 0;
	width: 200px;
	font-size: 18px;
	cursor: pointer;
}
.btn-confirm {
	margin: 0 5px;
	border: 1px solid #306eff;
	background: #fff;
}
.btn-cancel {
	margin: 0 5px;
	border: none;
	background: #306eff;
	color: #fff;
}
</style>