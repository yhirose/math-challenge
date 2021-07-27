<script lang="ts">
	import Header from './Header.svelte';
	import Problem from './Problem.svelte';
	import KeyPad from './KeyPad.svelte';
	import StartButton from './StartButton.svelte';
	import StopButton from './StopButton.svelte';
	import Score from './Score.svelte';
	import FanShape from './FanShape.svelte';

	let problems = [{ opr1: 0, opr2: 0, ope: '+', score: 0 }];
	let problemIndex = 0;
	let ans = '';
	let timeCount = 10;
	let timer = null;
	let startLabel = 'Start';
	let modes = [
		{ id: 0, value: 'Easy', maxNumber: 9 },
		{ id: 1, value: 'Normal', maxNumber: 25 },
		{ id: 2, value: 'Hard', maxNumber: 99 }
	];
	let modeSelected = 0;

	$: opr1 = problems[problemIndex].opr1;
	$: opr2 = problems[problemIndex].opr2;
	$: ope = problems[problemIndex].ope;
	$: totalScore = problems.reduce((acc, val) => acc + val.score, 0);

	function generateProblems() {
		const result = [];
		while (result.length < 10) {
			const { maxNumber } = modes[modeSelected];
			const opr1 = 1 + Math.floor(Math.random() * maxNumber);
			const opr2 = 1 + Math.floor(Math.random() * maxNumber);
			result.push({ opr1, opr2, ope: '+', score: 0 });
		}
		return result;
	}

	function start() {
		problems = generateProblems();
		problemIndex = 0;
		ans = '';
		timeCount = 10;
		timer = setInterval(() => {
			timeCount--;
			if (timeCount === 0) {
				resolved();
			}
		}, 1000);
	}

	function done() {
		window.clearInterval(timer);
		timer = null;
	}

	function isCorrect() {
		if (ope === '+') {
			return opr1 + opr2 === Number(ans);
		}
		return false;
	}

	function resolved() {
		const score = isCorrect() ? timeCount : 0;
		problems[problemIndex].score = score;

		setTimeout(() => {
			if (problemIndex + 1 < problems.length) {
				problemIndex++;
				ans = '';
				timeCount = 10;
			} else {
				done();
				if (totalScore < 10) {
					startLabel = 'Hello?';
				} else if (totalScore < 30) {
					startLabel = 'Needs work!';
				} else if (totalScore < 50) {
					startLabel = "Don't mind!";
				} else if (totalScore < 70) {
					startLabel = 'Pretty good!';
				} else if (totalScore < 80) {
					startLabel = 'Good Job!';
				} else if (totalScore < 90) {
					startLabel = 'Excellent!';
				} else {
					startLabel = 'Wow!';
				}
			}
		}, 300);
	}

	function handleKey(event) {
		const { key } = event.detail;
		switch (key) {
			case 'bs':
				if (ans.length > 0) {
					ans = ans.slice(0, -1);
				}
				break;
			case 'clr':
				ans = '';
				break;
			default:
				if (ans.length < 3) {
					ans += key;
				}
				break;
		}
		if (isCorrect()) {
			resolved();
		}
	}

	function handleStop() {
		done();
		startLabel = 'Try again?';
	}
</script>

<main>
	<Header>
		{#if timer}
			<StopButton on:click={handleStop}/>
		{:else}
			<div></div>
		{/if}
		<Score score={totalScore}/>
	</Header>
	<div class="content">
		{#if timer}
			<div class="problem">
				<Problem opr1={opr1} opr2={opr2} ope={ope} ans={ans}/>
			</div>
			<div class="fanshape">
				<FanShape degree={360 - timeCount * 36} fill="#888"/>
			</div>
		{:else}
			<StartButton on:click={start}>{@html startLabel}</StartButton>
			<div class="mode">
				<select bind:value={modeSelected}>
					{#each modes as mode}
						<option value={mode.id}>{mode.value}</option>
					{/each}
				</select>
			</div>
		{/if}
	</div>
	<KeyPad on:key={handleKey}/>
</main>

<style>
	main {
		display: grid;
		grid-template-rows: auto 1fr auto;

		height: 100%;
		background-color: whitesmoke;

		max-height: 960px;
		max-width: 480px;
		position: fixed;
		inset: 0;
		margin: auto;
	}

	.content {
		position: relative;
		display: grid;
		place-items: center;
	}

	.problem {
		position: relative;
	}

	.fanshape {
		height: 32px;
		width: 32px;
		position: absolute;
		top: 24px;
		right: 24px;
	}

	.mode {
		position: absolute;
		bottom: 24px;
	}
</style>
