<script lang="ts">
	import { onMount, onDestroy } from 'svelte';

	let days = '00';
	let hours = '00';
	let minutes = '00';
	let seconds = '00';

	const targetDate = new Date('2025-12-31T00:00:00');

	let interval: number;

	function updateTimer() {
		const now = new Date().getTime();
		const diff = targetDate.getTime() - now;

		if (diff <= 0) {
			days = hours = minutes = seconds = '00';
			clearInterval(interval);
			return;
		}

		const d = Math.floor(diff / (1000 * 60 * 60 * 24));
		const h = Math.floor((diff / (1000 * 60 * 60)) % 24);
		const m = Math.floor((diff / (1000 * 60)) % 60);
		const s = Math.floor((diff / 1000) % 60);

		days = String(d).padStart(2, '0');
		hours = String(h).padStart(2, '0');
		minutes = String(m).padStart(2, '0');
		seconds = String(s).padStart(2, '0');
	}

	onMount(() => {
		updateTimer();
		interval = setInterval(updateTimer, 1000);
	});

	onDestroy(() => {
		clearInterval(interval);
	});
</script>

<main class="container">
	<div class="content">
		<h1 class="fansytext">
			Академия Средиземья<br />
			<span>имени Финрода Фелагунда</span>
		</h1>

		<p class="subtitle fansytext">вновь откроет свои двери</p>

		<div class="divider">
			<span>◆</span>
			<span class="fansytext">до открытия</span>
			<span>◆</span>
		</div>

		<div class="timer">
			<div class="card">
				<div class="value fansytext">{days}</div>
				<div class="label fansytext">дней</div>
			</div>

			<div class="card">
				<div class="value fansytext">{hours}</div>
				<div class="label fansytext">часов</div>
			</div>

			<div class="card">
				<div class="value fansytext">{minutes}</div>
				<div class="label fansytext">минут</div>
			</div>

			<div class="card">
				<div class="value fansytext">{seconds}</div>
				<div class="label fansytext">секунд</div>
			</div>
		</div>

		<div class="quote fansytext">“Знания — свет, что никогда не угаснет”</div>
	</div>
</main>

<style>
	@import url('https://fonts.googleapis.com/css2?family=Comforter&family=Russo+One&display=swap');

	:global(body) {
		margin: 0;
		background: radial-gradient(circle at top, #442719, #120a06);
		color: #f6d27a;
		font-family: 'Cinzel', serif;
	}

	.container {
		min-height: 100vh;
		display: flex;
		align-items: center;
		justify-content: center;
		padding: 40px;
	}

	.content {
		text-align: center;
		max-width: 900px;
	}

	h1 {
		font-size: 4.5rem;
		font-weight: 600;
		margin-bottom: 20px;
	}

	h1 span {
		display: block;
		margin-top: 10px;
		font-size: 3rem;
	}

	.subtitle {
		font-size: 2rem;
		letter-spacing: 0.1em;
		color: #e8d8a8;
		margin-bottom: 40px;
	}

	.divider {
		display: flex;
		align-items: center;
		justify-content: center;
		gap: 16px;
		margin-bottom: 40px;
		color: #cfa64a;
		text-transform: uppercase;
		font-size: 0.8rem;
		letter-spacing: 0.2em;
	}

	.timer {
		display: grid;
		grid-template-columns: repeat(4, 1fr);
		gap: 24px;
		margin-bottom: 40px;
	}

	.card {
		background: linear-gradient(180deg, #5a1e1e, #3b1414);
		border-radius: 7px;
		padding: 30px 20px;
		box-shadow:
			inset 0 0 20px rgba(255, 200, 80, 0.15),
			0 0 25px rgba(0, 0, 0, 0.6);
	}

	.value {
		font-size: 3rem;
		font-weight: 700;
		color: #ffd56a;
		text-shadow: 0 0 12px rgba(255, 213, 106, 0.6);
	}

	.label {
		margin-top: 10px;
		font-size: 0.8rem;
		letter-spacing: 0.2em;
		text-transform: uppercase;
		color: #e0c98c;
	}

	.quote {
		margin-top: 20px;
		font-size: 1.5rem;
		font-style: italic;
		color: #bfa76a;
	}

    .fansytext {
  font-family: "Comforter", cursive;
  font-weight: 400;
  font-style: normal;
}

</style>
