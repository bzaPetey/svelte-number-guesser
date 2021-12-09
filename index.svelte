<script>
	let lo = 1;
	let hi = 100;
	let guess = 0;
	let guessCount = 0;
	let isReady = false;
	let isGameOver = false;

	function onLower() {
		hi = guess - 1;
		getGuess();
	}
	function onHigher() {
		lo = guess + 1;
		getGuess();
	}
	function onGotIt() {
		isGameOver = true;
	}
	function getGuess() {
		guess = Math.floor((lo + hi) / 2);
		guessCount++;
	}
	function onReady() {
		isReady = true;
		getGuess();
	}
	function resetGame() {
		lo = 1;
		hi = 100;
		guess = 0;
		guessCount = 0;
		isReady = false;
		isGameOver = false;
	}
</script>

<h1>Number Guesser</h1>
{#if isGameOver === false}
	{#if isReady === false}
		<p>Think of a number from {lo}-{hi} and I will guess it in 7 or fewer guesses.</p>
		<button on:click={onReady}>Click When Ready</button>
	{:else}
		<h3>Guess Count: {guessCount}</h3>
		<p>I guess {guess}. Is your number lower or higher?</p>
		<button on:click={onLower}>Lower</button>
		<button on:click={onHigher}>Higher</button>
		<button on:click={onGotIt}>Got It</button>
	{/if}
{:else}
	<p>I guessed {guess} in {guessCount} guesses.</p>
	<button on:click={resetGame}>Play Again</button>
{/if}
