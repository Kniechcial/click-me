<template>
	<div class="main-box">
		<div class="header-box">
			<p class="header-text">Would you like to see my Hungry app?</p>
		</div>
		<div class="button-box">
			<button
				ref="noButton"
				id="No-button"
				class="cloud-button"
				:class="[isButtonHovered ? 'dynamic-position' : 'initial-position']"
				@mouseover="
					isButtonHovered = true;
					buttonMove(noButton);
				"
				:style="{
					top: buttonPosition.top + 'px',
					left: buttonPosition.left + 'px',
				}">
				No :(
			</button>
			<button
				id="Yes-button"
				class="cloud-button"
				@click="toggleToHungry()">
				Yes :)
			</button>
		</div>
	</div>

	<Confetti :showConfetti="showConfetti"></Confetti>
	<BackgroundClouds></BackgroundClouds>
</template>

<script setup>
import { onMounted, ref } from "vue";
import BackgroundClouds from "./BackgroundClouds.vue";
import Confetti from "../views/Confetti.vue";

const showConfetti = ref(false);
const isButtonHovered = ref(false);
const noButton = ref(null);
const buttonPosition = ref({ top: 400, left: 0 });

onMounted(() => {
	isButtonHovered.value = false;
	buttonPosition.value = { top: 400, left: window.innerWidth / 2 - 100 };
});

const getRandomNumber = (number) => {
	return Math.floor(Math.random() * (number + 1));
};

const buttonMove = (element) => {
	const newTop = getRandomNumber(
		window.innerHeight - element.offsetHeight - 20
	);
	const newLeft = getRandomNumber(window.innerWidth - element.offsetWidth - 20);

	element.style.backgroundColor = "rgb(253, 12, 12)";
	buttonPosition.value.top = newTop;
	buttonPosition.value.left = newLeft;

	setTimeout(() => {
		element.style.backgroundColor = "rgb(71, 232, 71)";
	}, 500);
};

const toggleToHungry = () => {
	showConfetti.value = true;
	setTimeout(() => {
		window.location.href = "https://hungry-19f55.web.app/";
	}, 3000);
};
</script>

<style scoped>
* {
	box-sizing: border-box;
}
.main-box {
	display: flex;
	flex-direction: column;
	align-items: center;
	justify-content: center;
	height: 100vh;
}

.header-box {
	position: fixed;
	top: 10rem;
	padding: 10px 20px;
	text-align: center;
}

.header-text {
	font-family: "Oi", serif;
	font-weight: 400;
	font-style: normal;
	font-size: 40px;
	color: #001f3f;
}

.button-box {
	position: fixed;
	bottom: 20px;
	display: flex;
	justify-content: center;
}

#No-button,
#Yes-button {
	position: fixed;
	padding: 15px 25px;
	border: none;
	border-radius: 5px;
	cursor: pointer;
	color: black;
	font-weight: bold;
	font-size: large;
	z-index: 2;
	margin: 0 30px;
	transition: background-color 0.5s, top 1.5s, left 1.5s;
}

#No-button {
	top: 400px;
	left: calc(50% - 100px);
}

#Yes-button {
	top: 400px;
	left: calc(50% + 30px);
}

.dynamic-position {
	transition: background-color 0.5s;
}
.cloud-button {
	width: 100px;
	height: 53px;
	position: relative;
	border: none;
	cursor: pointer;
	display: inline-block;
	text-align: center;
	font-size: 1.5rem;
	color: #000;
	background-color: transparent;
	mask-image: url("../assets/cloud_button.png");
	mask-size: cover;
	mask-position: center;
	mask-repeat: no-repeat;
	-webkit-mask-image: url("../assets/cloud_button.png");
	-webkit-mask-size: cover;
	-webkit-mask-position: center;
	-webkit-mask-repeat: no-repeat;
	background: linear-gradient(
		to bottom,
		rgba(255, 255, 255, 0.8),
		rgba(173, 216, 230, 1)
	);
	transition: background-color 0.5s ease;
	box-shadow: 0 4px 10px rgba(0, 0, 0, 0.2);
}

#No-button.cloud-button:hover {
	background: linear-gradient(
		to bottom,
		rgba(105, 105, 105, 0.9),
		rgba(169, 169, 169, 1)
	);
}

#Yes-button.cloud-button:hover {
	background: linear-gradient(
		to bottom,
		rgba(255, 255, 153, 0.8),
		rgba(255, 255, 204, 1)
	);
}

.cloud-button span {
	position: absolute;
	top: 50%;
	left: 50%;
	transform: translate(-50%, -50%);
	z-index: 1;
}
</style>
