<template>
	<div v-if="showConfetti">
		<div class="container-right">
			<div
				v-for="i in confettiElements"
				:key="i"
				class="confetti"
				:style="confettiStyle(i)"></div>
		</div>
		<div class="container-left">
			<div
				v-for="i in confettiElements"
				:key="i"
				class="confetti"
				:style="confettiStyle(i)"></div>
		</div>
	</div>
</template>

<script setup>
const props = defineProps({
	showConfetti: Boolean,
});

const confettiElements = 32;
const confettiStyle = (i) => {
	const confettiPosition = i / confettiElements;
	const confettiColour = Math.random();
	return {
		"--confettiIndex": i,
		"--confettiPosition": confettiPosition,
		"--confettiColour": confettiColour,
	};
};
</script>

<style scoped>
.container-left {
	position: absolute;
	top: 50%;
	left: 7rem;
	transform: translateY(-50%) rotate(15deg);
	width: 100px;
	height: 100px;
}

.container-right {
	position: absolute;
	top: 50%;
	right: 17rem;
	transform: translateY(-50%) rotate(-15deg);
	width: 100px;
	height: 100px;
}

.confetti {
	--confettiColour: 0.5;
	--random-sine: calc((var(--confettiColour) - 0.5) * 2);

	position: absolute;
	top: 0;
	left: 50%;
	width: calc(
		60px + (var(--confettiPosition) * 200px) + calc(var(--confettiColour) * 10%)
	);
	height: calc((var(--confettiColour) * 120px) + 170px);

	border-radius: 40% 90% 0 0;
	pointer-events: none;

	--color: calc(var(--confettiColour) * 1turn) 85% 60%;
}

.confetti:nth-child(even) {
	transform: scale(-1, 1);
	left: auto;
	right: 50%;
}

.confetti::before {
	content: "";
	display: block;
	width: 14px;
	height: 7px;
	background-color: hsl(var(--color));

	animation: confetti 2s cubic-bezier(0.5, 0, 0.5, 1) both,
		confetti-opacity 2s cubic-bezier(0.5, 0, 0.5, 1) both;

	animation-duration: calc(2s + (var(--confettiColour) * 0.5s));
	animation-delay: calc(0.6s * var(--random-sine));
	animation-iteration-count: infinite;
	offset-path: padding-box;
}

@keyframes confetti-opacity {
	0% {
		opacity: 0;
	}
	20%,
	40% {
		opacity: 1;
	}
	95%,
	100% {
		opacity: 0;
	}
}

@keyframes confetti {
	0% {
		offset-distance: -15%;
		offset-rotate: 0turn;
	}
	100% {
		offset-distance: 40%;
		offset-rotate: calc(4turn + var(--confettiColour) * 2turn);
	}
}
</style>
