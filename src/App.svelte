<script>
  let px = 10;
	let baseSize = 16;

	$: rem = px / baseSize;

	function getTailwindValue(px) {
		if( px < 1 ) return px;
		const theoreticalValue = rem * 4;
		const possibleValues = [0.5, 1, 1.5, 2, 2.5, 3, 3.5, 4, 5, 6, 7, 8 ,9, 10, 11, 12, 14, 16, 20, 24 ,28, 32, 36, 40, 44, 48, 52, 56, 60, 64, 72, 80, 96];
		if ( possibleValues.includes(theoreticalValue) ) return theoreticalValue;
		const closest = possibleValues.sort((a, b) => { return Math.abs(theoreticalValue - a) - Math.abs(theoreticalValue - b) })[0]
		return `${ closest } (approx)`
	}

	$: tailwindValue = getTailwindValue(px)

	function tailwindValue() {
		if(px<1) return px;
	}
</script>

<main>
	<div class="block">
		<h1>Tailwind calculator</h1>
		<p>Input your pixels, and get the number on your Tailwind classes (if you use the default sizing)</p>
		<div class="row">
			<label class="row__label" for="px">Pixels:</label>
			<input class="row__value" type="number" bind:value={px}/>
		</div>
		<div class="row">
			<span class="row__label">REM:</span>
			<span class="row__value">{ rem }</span>
		</div>
		<div class="row">
			<span class="row__label">Tailwind:</span>
			<span class="row__value">{ tailwindValue }</span>
		</div>
	</div>
</main>

<style>
	main {
		text-align: center;
		height: 100vh;
		display: flex;
		align-items: center;
		justify-content: center;
	}

	.block{
		max-width: 240px;
		background: #DDEEFF;
		padding: 2rem 3rem;
		border-radius: 1.5rem;
		box-shadow: 0 5px 5px #012;;
	}

	.row{
		display: flex;
		flex-direction: row;
		justify-content: center;
		align-items: center;
		gap: 1rem;
		margin: 1rem 0;
	}

	.row__label{
		width: 3rem;
		text-align: right;
		color: #456;
	}

	.row__value{
		background: white;
		border-radius: 0.25rem;
		width: 10rem;
		text-align: left;
		box-sizing: border-box;
		padding: 0.5rem 1rem;
		margin: 0;
		border: solid 1px #abc;
		color: #123;
		box-shadow: inset 0 1px 2px #abc;
	}

	h1 {
		color: #789;
		text-transform: uppercase;
		font-size: 2.5em;
		font-weight: 200;
		margin: 1rem 0 2rem;
	}
	p {
		color: #789;
		text-align: left;
		padding-bottom: 2rem;
		border-bottom: solid 1px #789;
		margin-bottom: 2rem;
	}

</style>
