<template>
	<div
		v-for="(cloud, index) in clouds"
		:key="index"
		class="cloud-box"
		:style="{
			top: cloud.top + 'px',
			left: '100vw',
			animationDuration: cloud.animationDuration + 's',
		}">
		<div class="cloud">
			<img
				src="../assets/cloud.png"
				alt="Chmura"
				:style="{
					width: cloud.width + 'px',
					height: cloud.height + 'px',
				}" />
		</div>
	</div>
</template>

<script setup>
import { ref, onMounted } from "vue";

const clouds = ref([]);

const generateCloud = () => {
	const sizeMultiplier = Math.random() * 0.4 + 1.5;
	const newCloud = {
		top: Math.floor(Math.random() * window.innerHeight * 0.7),
		width: 100 * sizeMultiplier,
		height: 80 * sizeMultiplier,
		animationDuration: Math.floor(Math.random() * 10) + 25,
	};
	clouds.value.push(newCloud);

	setTimeout(() => {
		const index = clouds.value.indexOf(newCloud);
		if (index !== -1) {
			clouds.value.splice(index, 1);
		}
	}, newCloud.animationDuration * 1000);
};

const startGeneratingClouds = () => {
	const minTime = 2000;
	const maxTime = 5000;

	const generateRandomCloud = () => {
		generateCloud();
		const randomDelay =
			Math.floor(Math.random() * (maxTime - minTime + 1)) + minTime;
		setTimeout(generateRandomCloud, randomDelay);
	};

	generateRandomCloud();
};

onMounted(() => {
	startGeneratingClouds();
});
</script>

<style scoped>
.cloud-box {
	animation: float linear infinite;
	position: fixed;
	top: 10rem;
	right: 1rem;
}

.cloud {
	height: 8rem;
	width: 11rem;
	overflow: hidden;
}

.cloud img {
	height: 100%;
	width: 100%;
	object-fit: cover;
}

@keyframes float {
	0% {
		transform: translateX(0);
	}
	100% {
		transform: translateX(-200vw);
	}
}
</style>
