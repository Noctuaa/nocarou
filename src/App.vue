<template>
	<div class="bar"></div>
	<div class="container">
		<div class="wrapper">
			<div class="features text-center">
				<h1 class="text-center">Nocarou</h1>
				<h2>Features</h2>
				<hr>
				<ul>
					<li>Single slide</li>
					<li>Multiple slides</li>
					<li>Loop</li>
					<li>Arrow key Navigation</li>
				</ul>
			</div>
			<div class="main">
				<div class="title">
					<h2 class="text-center">Single Item</h2>
				</div>
				<div class="single">
					<Carousel v-bind:itemsToScroll="1" v-bind:itemsToShow="1">
						<CarouselSlide v-for="i in 5" :index="i - 1" :key="i">
							<img :src="'https://picsum.photos/600/400?random=' + i" alt="">
						</CarouselSlide>
					</Carousel>
				</div>
				<div class="title">
					<h2 class="text-center">Multiple items loop</h2>
				</div>
				<Carousel v-bind:loop="true" v-bind:itemsToScroll="2" v-bind:itemsToShow="3">
					<CarouselSlide v-for="i in 9" :index="i - 1" :key="i">
						<img :src="'https://picsum.photos/600/400?random=' + i" alt="">
					</CarouselSlide>
				</Carousel>
			</div>
		</div>
	</div>
</template>

<script>
	import Carousel from './components/carousel/Carousel';
	import CarouselSlide from './components/carousel/CarouselSlide';

	export default {
		name: 'App',
		components: {
			Carousel,
			CarouselSlide
		},
		data() {
			return {
			}
		}
	}
</script>

<style lang="scss">
	@import '@/sass/app.scss';
</style>