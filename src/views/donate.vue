<template>
	<div class="container">
		<div class="plugins-tips">
			如果该框架对你有帮助，那就请作者喝杯饮料吧！<el-icon><ColdDrink /></el-icon> 加微信号<span>Delon2030</span><i style="cursor: pointer; margin: 0 6px; color: #409eff" class="el-icon-lx-copy" @click="copy"></i> 探讨问题。
		</div>
		<div>
			<img style="width: 300px" src="src/assets/img/wechat.png" />
		</div>
	</div>
</template>

<script setup lang="ts" name="donate">
import { ElMessage } from 'element-plus';

const copy = () => {
	ElMessage.success('复制成功');
	navigator.clipboard.writeText('Delon2030');
};
</script>

<style></style>
