<template>
	<div id="app">

		<transition :name="transitionName">
			<router-view class="child-view"></router-view>
		</transition>

	</div>
</template>

<script>
	export default {
		name: 'app',
		created() {
			try {
				document.body.removeChild(document.getElementById('appLoading'))
				setTimeout(function() {
					document.getElementById('app').className = "animated" + " " + "fadeIn"
				}, 500)
			} catch(e) {

			}
		},
		data() {
			return {
				transitionName: 'slide-left'
			}
		},
		mounted() {},
		//监听路由的路径，可以通过不同的路径去选择不同的切换效果  
		watch: {
			'$route' (to, from) {
				if(to.path == '/') {
					this.transitionName = 'slide-right';
				} else {
					this.transitionName = 'slide-left';
				}
			}
		}
	}
</script>

<style>
	#app {
		opacity: 0;
	}
	
	.child-view {
		position: absolute;
		left: 0;
		top: 0;
		width: 100%;
		height: 100%;
		transition: all .5s cubic-bezier(0.420, 0.000, 1.000, 1.000);
	}
	
	.slide-left-enter,
	.slide-right-leave-active {
		opacity: 0;
		-webkit-transform: translate(30px, 0);
		transform: translate(30px, 0);
	}
	
	.slide-left-leave-active,
	.slide-right-enter {
		opacity: 0;
		-webkit-transform: translate(-30px, 0);
		transform: translate(-30px, 0);
	}
</style>