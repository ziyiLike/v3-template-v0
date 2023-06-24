<template>
	<div class="loading">Loading...</div>
	<div class="template-page">
		<div class="header">
			<div class="logo">GSAP</div>
			<nav>
				<ul>
					<li>Home</li>
					<li>About</li>
					<li>Contact</li>
				</ul>
			</nav>
		</div>

		<div class="content">
			<div class="left">
				<h2>Hellow Gsap</h2>
				<h2>This is a demo for gsap</h2>
				<h3>Enjoy it Magic Animation feature of gsap</h3>
			</div>
			<div class="right">
				<video
					class="active"
					src="/src/assets/spring.mp4"
					autoplay
					loop
					muted
				></video>
			</div>
		</div>
	</div>
</template>

<script setup lang="ts">
import gsap from 'gsap'
import { ScrollTrigger } from 'gsap/ScrollTrigger'

onMounted(() => {
	LoadAnimation()
})

const LoadAnimation = () => {
	const tl = gsap.timeline()

	tl.to('.loading', {
		duration: 0.5,
		opacity: 0,
		display: 'none',
		ease: 'power2',
	})
		.from('.header', {
			duration: 0.5,
			opacity: 0,
			y: -100,
			ease: 'back',
			stagger: 0.25,
		})
		.from('.left h2', {
			duration: 0.5,
			opacity: 0,
			y: 100,
			ease: 'back',
			stagger: 0.25,
		})
		.from(
			'.left h3',
			{
				duration: 0.5,
				opacity: 0,
				y: 100,
				ease: 'back',
				stagger: 0.25,
			},
			'-=0.5'
		)
		.from(
			'.right video',
			{
				duration: 1,
				opacity: 0,
				y: 100,
				ease: 'back',
				stagger: 0.25,
			},
			'-=0.5'
		)

	gsap.registerPlugin(ScrollTrigger)
	gsap.to('.right', {
		scale: 1,
		x: 0,
		y: 0,
		scrollTrigger: {
			trigger: '.content',
			start: 'bottom bottom',
			end: 'bottom top',
			scrub: true,
			pin: true,
			markers: false,
		},
	})

	// const dom = document.querySelector('.car-box')
	// const effect = gsap.to(dom, {
	// 	duration: 5,
	// 	x: 100,
	// 	y: 600,
	// 	repeat: -1,
	// 	repeatDelay: 1,
	// })
}
</script>

<style lang="scss">
.template-page {
	width: 100%;
	min-height: 100vh;
}

.header {
	display: flex;
	justify-content: space-between;
	align-items: center;
	padding: 20px 40px;
	background-color: #fff;
	box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);

	.logo {
		font-size: 30px;
		font-weight: bold;
	}

	nav {
		ul {
			display: flex;

			li {
				margin-left: 20px;
				cursor: pointer;

				&:hover {
					color: #1890ff;
				}
			}
		}
	}
}

.content {
	display: flex;
	justify-content: space-between;
	align-items: center;
	padding: 20px 40px;
	position: relative;
	overflow: hidden;
	min-height: 800px;

	.left {
		position: absolute;
		top: 20%;

		h2 {
			font-size: 30px;
			font-weight: bold;
			margin-bottom: 20px;
		}

		h3 {
			font-size: 25px;
		}
	}

	.right {
		overflow: hidden;
		position: absolute;
		right: 40px;
		border-radius: 20px;
		width: 1000px;
		height: 800px;
		transform: translate(800px, 400px) scale(2, 2);

		video {
			width: 100%;
			height: 100%;
		}
	}
}

.loading {
	position: fixed;
	top: 0;
	left: 0;
	width: 100%;
	height: 100vh;
	display: flex;
	justify-content: center;
	align-items: center;
	font-size: 30px;
	font-weight: bold;
	z-index: 999;
	background: #f1d6f1;
}
</style>
