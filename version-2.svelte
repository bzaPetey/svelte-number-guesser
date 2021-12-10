<script lang="ts">
	let lo = 1;
	let hi = 100;
	let guess = -1;
	let isReady = false;
	let isGameOver = false;
	let guessCount = 0;

	function getGuess() {
		guess = Math.floor((lo + hi) / 2);
		guessCount++;
	}

	function newGame() {
		lo = 1;
		hi = 100;
		isReady = false;
		isGameOver = false;
		guessCount = 0;
	}
</script>

<h1>Number Guesser</h1>
{#if isReady === false}
	<p>Think of a number from {lo}-{hi} and I will guess it in 7 or fewer guesses.</p>
	<button on:click={() => {isReady = true; getGuess()}}>Click When Ready</button>
{:else}
	<h3>Guess Count: {guessCount}</h3>
	<p>My guess is {guess}. Is your number higher or lower?</p>
	<p>
		<button on:click={() => {hi = guess - 1; getGuess()}}>Lower</button>
		<button on:click={() => {lo = guess + 1; getGuess()}}>Higher</button>
		<button on:click={() => {isGameOver = true}}>Guessed It</button>
	</p>
{/if}

{#if isGameOver === true}
	<p>I guessed the number {guess} in {guessCount}.</p>
	<button on:click={newGame}>New Game</button>
{/if}
  
