<script>
	import { Copy } from 'lucide-svelte';
	let pass = '';
	let numberAllowed = false;
	let charAllowed = false;

	let length = 4;

	function passwordGen() {
		let generatedPass = '';
		let str = 'ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz';
		if (numberAllowed) str += '0123456789';
		if (charAllowed) str += '!@#$%^&*-_+=[]{}~`';

		for (let i = 1; i <= length; i++) {
			let char = Math.floor(Math.random() * str.length + 1);
			generatedPass += str.charAt(char);
		}
		console.log(generatedPass + ' ' + length);
		pass = generatedPass;
	}
	
</script>

<h3>Password Generator</h3>

<div id="input-card">
	<input bind:value={pass} disabled type="text" />
	<button> <Copy /> </button>
</div>

<br />

<div id="card">
	<div>
		<input
			bind:value={length}
			on:input={passwordGen}
			min={4}
			max={20}
			type="range"
			name="charLength"
		/>
		<label for="charLength">Character Length : {length}</label>
	</div>

	<div>
		<input bind:checked={numberAllowed} on:click={passwordGen} type="checkbox" name="numbers" />
		<label for="numbers">Number allowed?</label>
		<br />
		<input bind:checked={charAllowed} on:click={passwordGen} type="checkbox" name="numbers" />
		<label for="numbers">Special Characters allowed?</label>
		<br />
	</div>
</div>

<style>
	input[type='text'],
	button {
		all: unset;
		width: 40%;
	}

	input[type='text'] {
		border-bottom: 1px solid #ccc;
	}

	button {
		color: white;
		padding: 10px 20px;
		border: none;
		cursor: pointer;
	}
	
	#card,
	#input-card {
		
		padding: 2rem;
		width: 100%;
		border: black solid;
		background-color: #24232b;
		transition: width 0.2s ease-in-out;
	}
	input[type='range'],
	input[type='checkbox'] {
		accent-color: #a5ffad;
	}
	input[type='range'] {
		transition: all 0.2s ease-in-out;
	}
</style>
