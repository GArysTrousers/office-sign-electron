<script lang="ts">
	import type { Message } from 'src/lib/interfaces';
	import { onMount } from 'svelte';

	export let messages: Message[] = [
		{
			title: 'ICT is Closed\nfor the day',
			body: '',
			bg: 'bg-black',
			onStart: () => {},
			onTimeout: () => {},
			onEnd: () => {},
		},
		{
			title: 'ICT is Open',
			body: 'Turn handle &#8634;',
			bg: 'bg-green-700',
			onStart: () => {},
			onTimeout: () => {},
			onEnd: () => {},
		},
		{
			title: 'ICT is Closed',
			body: 'Check back later \n-or-\n see Junior ICT',
			bg: 'bg-red-700',
			onStart: () => {},
			onTimeout: () => {},
			onEnd: () => {},
		},
		{
			title: 'ICT is Closed',
			body: 'Check back in:',
			bg: 'bg-red-700',
			onStart: () => addTime(60 * 30),
			onTimeout: () => changeMessage(4),
			onEnd: () => {},
		},
		{
			title: 'ICT will be back shortly',
			body: '',
			bg: 'bg-yellow-600',
			onStart: () => {},
			onTimeout: () => {},
			onEnd: () => {},
		},
	];

	let selected = messages[1];
	let timer: any;
	let timeLeft: number = 0;

	onMount(async () => {});

	function changeMessage(index: number) {
		stopTimer();
		selected.onEnd();
		selected = messages[index];
		selected.onStart();
	}

	function addTime(length: number) {
		clearInterval(timer);
		timeLeft += length;
		timer = setInterval(() => {
			timeLeft -= 1;
			if (timeLeft <= 0) {
				clearInterval(timer);
				selected.onTimeout();
			}
		}, 1000);
	}

	function stopTimer() {
		clearInterval(timer);
		timeLeft = 0;
	}

	function convertToTime(time: number) {
		return `${Math.floor(time / 60)}:${String(time % 60).padStart(2, '0')}`;
	}

	function onKeyDown(e: KeyboardEvent) {
		let num = e.keyCode - 48;
		if (num >= 0 && num <= 9) {
			if (num < messages.length) changeMessage(num);
			return;
		}
		if (e.key == ' ') addTime(600);
		else if (e.key == 'Backspace') stopTimer();
		else if (window.electron && e.key == 'Escape') window.electron.send('to-main', 'close');
	}
</script>

<svelte:window on:keydown={onKeyDown} />

<main class="{selected.bg} ">
	<div class="flex-col justify-center items-center">
		<h1 class="title mb-6">{@html selected.title}</h1>
		<div class="body">{@html selected.body}</div>
		{#if timeLeft > 0}
			<div class="text-9xl">{convertToTime(timeLeft)}</div>
		{/if}
	</div>
</main>

<style>
	main {
		height: 100vh;
		@apply text-white flex flex-col justify-center items-center text-center whitespace-pre-wrap;
	}

	.title {
		font-size: 13vw;
	}

	.body {
		font-size: 5vw;
	}
</style>
