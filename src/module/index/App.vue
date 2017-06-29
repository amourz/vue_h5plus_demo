<template>
	<div>
		<div class="vux-demo">
			<img class="logo" src="../../assets/vux_logo.png">
			<h1> </h1>
		</div>
		<group v-bind:title="msg">
			<cell title="Vux" value="Cool" is-link></cell>
		</group>
	</div>
</template>

<script>
	import { Group, Cell } from 'vux'

	const plusReady = function(fn) {
		if(window.plus) {
			setTimeout(fn, 0)
		} else {
			document.addEventListener("plusready", fn, false)
		}
	}

	export default {
		components: {
			Group,
			Cell
		},
		data() {
			return {
				// note: changing this line won't causes changes
				// with hot-reload because the reloaded component
				// preserves its current state and we are modifying
				// its initial state.
				msg: 'Hello World!'
			}
		},
		created() {
			plusReady(this.init);
		},
		methods: {
			init() {
				this.msg = plus.device.uuid
				let url = 'http://www.wondfun.com/look/sendMsg.php'
				this.$http.post(url, {})
					.then(function(res) {
						console.log(JSON.stringify(res));
					})
					.catch(function(err) {
						console.log(err);
					})
			}
		}
	}
</script>

<style>
	.vux-demo {
		text-align: center;
	}
	
	.logo {
		width: 100px;
		height: 100px
	}
</style>