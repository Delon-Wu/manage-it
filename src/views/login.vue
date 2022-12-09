<template>
	<div class="login-wrap section">
		<img class="logo" src="src\assets\img\logo_transparent.png" alt="">
		<div class="login-wrap_container">
			<div class="row full-height justify-content-center">
				<div class="text-center align-self-center">
					<div class="sectiontext-center">
						<h6 class="text-center mg-3"><span>登录 </span><span>注册</span></h6>
						<input class="checkbox" type="checkbox" id="reg-log" name="reg-log" />
						<label class="switch-label" for="reg-log"></label>
						<div class="card-3d-wrap mx-auto">
							<div class="card-3d-wrapper">
								<div class="card-front">
									<div class="center-wrap">
										<div class="section text-center">
											<h4>登录</h4>
											<div class="form-group">
												<input type="email" name="logemail" class="form-style"
													placeholder="Your Username" id="logemail" autocomplete="off"
													v-model="param.username">
												<i class="input-icon el-icon-lx-people"></i>
											</div>
											<div class="form-group">
												<input type="password" name="logpass" class="form-style"
													placeholder="Your Password" id="logpass" autocomplete="off"
													v-model="param.password">
												<i class="input-icon el-icon-lx-lock"></i>
											</div>
											<a href="#" class="btn mg-b2" @click="submitForm()">提交</a>
											<p class="mb-0 mt-4 text-center"><a href="#0" class="link">&nbsp;&nbsp;忘记密码？</a></p>
										</div>
									</div>
								</div>
								<div class="card-back">
									<div class="center-wrap">
										<div class="section text-center">
											<h4 class="mb-4 pb-3">注册</h4>
											<div class="form-group">
												<input type="text" name="logname" class="form-style"
													placeholder="Your Full Name" id="logname" autocomplete="off"
													v-model="param.username">
												<i class="input-icon el-icon-lx-people"></i>
											</div>
											<div class="form-group">
												<input type="email" name="logemail" class="form-style"
													placeholder="Your Email" id="logemail" autocomplete="off"
													v-model="param.email">
												<i class="input-icon el-icon-lx-mail"></i>
											</div>
											<div class="form-group">
												<input type="password" name="logpass" class="form-style"
													placeholder="Your Password" id="logpass" autocomplete="off"
													v-model="param.password">
												<i class="input-icon el-icon-lx-lock"></i>
											</div>
											<a href="#" class="btn" @click="submitForm()">提交</a>
										</div>
									</div>
								</div>
							</div>
						</div>
					</div>
				</div>
			</div>
		</div>
	</div>
</template>

<script setup lang="ts">
import { ref, reactive } from 'vue';
import { useTagsStore } from '../store/tags';
import { usePermissStore } from '../store/permiss';
import { useRouter } from 'vue-router';
import { ElMessage } from 'element-plus';
import type { FormInstance, FormRules } from 'element-plus';

interface LoginInfo {
	username: string;
	password: string;
	email: string;
}

const router = useRouter();
const param = reactive<LoginInfo>({
	username: 'admin',
	password: '123123',
	email: '',
});

const permiss = usePermissStore();
const submitForm = (formEl: FormInstance | undefined) => {
	ElMessage.success('登录成功');
	localStorage.setItem('ms_username', param.username);
	const keys = permiss.defaultList[param.username == 'admin' ? 'admin' : 'user'];
	permiss.handleSet(keys);
	localStorage.setItem('ms_keys', JSON.stringify(keys));
	router.push('/');
};

const tags = useTagsStore();
tags.clearTags();
</script>

<style scoped>
@import url('https://fonts.googleapis.com/css?family=Poppins:400,500,600,700,800,900');
.login-wrap {
	position: relative;
	width: 100%;
	height: 100%;
	font-family: 'Poppins', sans-serif;
	font-weight: 300;
	font-size: 15px;
	line-height: 1.7;
	color: #c4c3ca;
	background-color: #1f2029;
	overflow-x: hidden;
}

.login-wrap_container {
	background: none;
	width: 100%;
    padding-right: 15px;
    padding-left: 15px;
    margin-right: auto;
    margin-left: auto;
}

@media (min-width: 1200px) {
	.login-wrap_container {
		max-width: 1140px;
	}
}

.row {
	display: -ms-flexbox;
    display: flex;
    -ms-flex-wrap: wrap;
    flex-wrap: wrap;
    margin-right: -15px;
    margin-left: -15px;
}

.justify-content-center {
	display: flex;
	justify-content: center;
}

.align-self-center {
	display: flex;
	align-self: center;
}

a {
	cursor: pointer;
	transition: all 200ms linear;
}

a:hover {
	text-decoration: none;
}

.link {
	color: #c4c3ca;
}

.link:hover {
	color: #ffeba7;
}

p {
	font-weight: 500;
	font-size: 14px;
	line-height: 1.7;
}

h4 {
	font-weight: 600;
	font-size: 1.5rem;
	margin-bottom: 1.5rem;
	padding-bottom: 1rem;
}

h6 span {
	padding: 0 20px;
	text-transform: uppercase;
	font-weight: 700;
	font-size: 1rem;
}

.section {
	position: relative;
	width: 100%;
	display: block;
}

.full-height {
	min-height: 100vh;
}

.text-center {
	text-align: center;
}

.mg-3 {
	margin: 3em;
}
.mg-b2 {
	margin-bottom: 2em;
}

[type="checkbox"]:checked,
[type="checkbox"]:not(:checked) {
	position: absolute;
	left: -9999px;
}

.checkbox:checked+label,
.checkbox:not(:checked)+label {
	position: relative;
	display: block;
	text-align: center;
	width: 60px;
	height: 16px;
	border-radius: 8px;
	padding: 0;
	margin: 10px auto;
	cursor: pointer;
	background-color: #ffeba7;
}

.checkbox:checked+label:before,
.checkbox:not(:checked)+label:before {
	content: '';
	position: absolute;
	display: block;
	background-image: url('/src/assets/img/long-arrow-down.png');
	background-size: 20px;
	background-position: center;
	background-repeat: no-repeat;
	transform: rotate(135deg);
	width: 36px;
	height: 36px;
	border-radius: 50%;
	color: #ffeba7;
	background-color: #102770;
	font-family: 'unicons';
	z-index: 20;
	top: -10px;
	left: -10px;
	line-height: 36px;
	text-align: center;
	font-size: 24px;
	transition: all 0.5s ease;
}

.checkbox:checked+label:before {
	transform: translateX(44px) rotate(-135deg);
}


.card-3d-wrap {
	position: relative;
	width: 440px;
	max-width: 100%;
	height: 400px;
	-webkit-transform-style: preserve-3d;
	transform-style: preserve-3d;
	perspective: 800px;
	margin-top: 60px;
}

.card-3d-wrapper {
	width: 100%;
	height: 100%;
	position: absolute;
	top: 0;
	left: 0;
	-webkit-transform-style: preserve-3d;
	transform-style: preserve-3d;
	transition: all 600ms ease-out;
}

.card-front,
.card-back {
	width: 100%;
	height: 100%;
	background-color: #2a2b38;
	background-image: url('https://s3-us-west-2.amazonaws.com/s.cdpn.io/1462889/pat.svg');
	background-position: bottom center;
	background-repeat: no-repeat;
	background-size: 300%;
	position: absolute;
	border-radius: 6px;
	left: 0;
	top: 0;
	-webkit-transform-style: preserve-3d;
	transform-style: preserve-3d;
	-webkit-backface-visibility: hidden;
	-moz-backface-visibility: hidden;
	-o-backface-visibility: hidden;
	backface-visibility: hidden;
}

.card-back {
	transform: rotateY(180deg);
}

.checkbox:checked~.card-3d-wrap .card-3d-wrapper {
	transform: rotateY(180deg);
}

.center-wrap {
	box-sizing: border-box;
	position: absolute;
	width: 100%;
	padding: 0 35px;
	top: 50%;
	left: 0;
	transform: translate3d(0, -50%, 35px) perspective(100px);
	z-index: 20;
	display: block;
}


.form-group {
	position: relative;
	display: block;
	margin: 0;
	margin-bottom: 1em;
	padding: 0;
}

.form-style {
	box-sizing: border-box;
	padding: 13px 20px;
	padding-left: 55px;
	height: 48px;
	width: 100%;
	font-weight: 500;
	border-radius: 4px;
	font-size: 14px;
	line-height: 22px;
	letter-spacing: 0.5px;
	outline: none;
	color: #c4c3ca;
	background-color: #1f2029;
	border: none;
	-webkit-transition: all 200ms linear;
	transition: all 200ms linear;
	box-shadow: 0 4px 8px 0 rgba(21, 21, 21, .2);
}

.form-style:focus,
.form-style:active {
	border: none;
	outline: none;
	box-shadow: 0 4px 8px 0 rgba(21, 21, 21, .2);
}

.input-icon {
	position: absolute;
	top: 0;
	left: 18px;
	height: 48px;
	font-size: 24px;
	line-height: 48px;
	text-align: left;
	color: #ffeba7;
	-webkit-transition: all 200ms linear;
	transition: all 200ms linear;
}


.form-group input:-ms-input-placeholder {
	color: #c4c3ca;
	opacity: 0.7;
	-webkit-transition: all 200ms linear;
	transition: all 200ms linear;
}

.form-group input::-moz-placeholder {
	color: #c4c3ca;
	opacity: 0.7;
	-webkit-transition: all 200ms linear;
	transition: all 200ms linear;
}

.form-group input:-moz-placeholder {
	color: #c4c3ca;
	opacity: 0.7;
	-webkit-transition: all 200ms linear;
	transition: all 200ms linear;
}

.form-group input::-webkit-input-placeholder {
	color: #c4c3ca;
	opacity: 0.7;
	-webkit-transition: all 200ms linear;
	transition: all 200ms linear;
}

.form-group input:focus:-ms-input-placeholder {
	opacity: 0;
	-webkit-transition: all 200ms linear;
	transition: all 200ms linear;
}

.form-group input:focus::-moz-placeholder {
	opacity: 0;
	-webkit-transition: all 200ms linear;
	transition: all 200ms linear;
}

.form-group input:focus:-moz-placeholder {
	opacity: 0;
	-webkit-transition: all 200ms linear;
	transition: all 200ms linear;
}

.form-group input:focus::-webkit-input-placeholder {
	opacity: 0;
	-webkit-transition: all 200ms linear;
	transition: all 200ms linear;
}

.btn {
	border-radius: 4px;
	height: 44px;
	font-size: 13px;
	font-weight: 600;
	text-transform: uppercase;
	-webkit-transition: all 200ms linear;
	transition: all 200ms linear;
	padding: 0 30px;
	letter-spacing: 1px;
	display: -webkit-inline-flex;
	display: -ms-inline-flexbox;
	display: inline-flex;
	-webkit-align-items: center;
	-moz-align-items: center;
	-ms-align-items: center;
	align-items: center;
	-webkit-justify-content: center;
	-moz-justify-content: center;
	-ms-justify-content: center;
	justify-content: center;
	-ms-flex-pack: center;
	text-align: center;
	border: none;
	background-color: #ffeba7;
	color: #102770;
	box-shadow: 0 8px 24px 0 rgba(255, 235, 167, .2);
}

.btn:active,
.btn:focus {
	background-color: #102770;
	color: #ffeba7;
	box-shadow: 0 8px 24px 0 rgba(16, 39, 112, .2);
}

.btn:hover {
	background-color: #102770;
	color: #ffeba7;
	box-shadow: 0 8px 24px 0 rgba(16, 39, 112, .2);
}




.logo {
	position: absolute;
	width: 120px;
	top: 30px;
	right: 30px;
	display: block;
	z-index: 100;
	transition: all 250ms linear;
	background-color: #ffeba7;
	border-radius: 10px;
}
</style>
