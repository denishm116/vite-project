<template>
	<div>
		<section>
			<div class="sk-three-bounce">
				<div class="sk-bounce-1 sk-child"></div>
				<div class="sk-bounce-2 sk-child"></div>
				<div class="sk-bounce-3 sk-child"></div>
			</div>
		</section>
	</div>
</template>

<style scoped lang="scss">
$spinkit-size: 2em !default;

section {
	flex: 1 1 25%;
}

.sk-three-bounce {
	$animationDuration: 1.4s;
	$delayRange: 0.32s;
	width: ($spinkit-size * 2);
	margin: 1em auto;
	text-align: center;

	.sk-child {
		width: calc($spinkit-size / 2);
		height: calc($spinkit-size / 2);
		background-color: #6d6d6d;

		border-radius: 100%;
		display: inline-block;
		animation: sk-three-bounce $animationDuration ease-in-out 0s infinite both;
	}

	.sk-bounce-1 {
		animation-delay: -$delayRange;
	}
	.sk-bounce-2 {
		animation-delay: calc($delayRange / 2);
	}
}

@keyframes sk-three-bounce {
	0%,
	80%,
	100% {
		transform: scale(0);
	}
	40% {
		transform: scale(1);
	}
}
</style>
