<script>
	import Loader from "./Loader.svelte";
	import WordData from "./WordData.svelte";
	let word = "";
	let loading = false;
	let wordData = null;

	async function searchWord(){
		if(word.length === 0){
			return;
		}
		loading = true;
		wordData = null;
		try {
			let res = await fetch("https://api.dictionaryapi.dev/api/v2/entries/en/"+word);
			let data = await res.json();
			if(Array.isArray(data)){
				wordData = data[0];
			} else{
				wordData = "No result";
			}
			loading = false;
		} catch(err){
			loading = false;
		}
	}
	
</script>

<style>
		/* Header styles */
		.header {
		font-size: 2rem;
		font-weight: bold;
		text-align: center;
		margin: 2rem 0;
	}

	/* Centering styles */
	.center {
		display: flex;
		flex-direction: column;
		align-items: center;
	}

	/* Form styles */
	.form {
		display: flex;
		flex-direction: column;
		align-items: center;
		margin-bottom: 1rem;
	}

	.form-group {
		margin-bottom: 1rem;
	}

	label {
		font-size: 1.2rem;
		font-weight: bold;
		margin-bottom: 0.5rem;
	}

	input[type="text"] {
		font-size: 1.2rem;
		padding: 0.5rem;
		border: 2px solid #ccc;
		border-radius: 5px;
	}

	button {
		font-size: 1.2rem;
		padding: 0.5rem 1rem;
		background-color: #007bff;
		color: #fff;
		border: none;
		border-radius: 5px;
		cursor: pointer;
	}

	/* Result styles */
	.result {
		margin-top: 2rem;
	}

	.padding {
		padding: 1rem;
	}
	footer {
  background-color: #f5f5f5;
  padding: 20px;
  text-align: center;
  font-size: 14px;
  position: fixed;
  bottom: 0;
  width: 100%;
}

footer p {
  margin: 0;
}

footer a {
  color: orangered;
  font-weight: bold;
  text-decoration: none;
  font-size: 1.5rem;
}

footer a:hover {
	color: rgb(255, 30, 0);
  font-size: 2rem;
}

</style>

<main>
	<div class="header">DOSU Dictionary App</div>
	<div class="center">
		<div class="form">
			<div class="form-group">
				<!-- svelte-ignore a11y-label-has-associated-control -->
				<label>Search Word</label>
				<input type="text" placeholder="Type here" bind:value={word}/>
			</div>
			<div class="form-group">
				<button on:click={searchWord}>Search</button>
			</div>
		</div>
		{#if loading === true || wordData !== null}
			<div class="result">
				{#if wordData !== null && typeof wordData !== "string"}
					<WordData wordData={wordData}/>
				{:else if wordData === null && loading === true}
					<Loader/>
				{:else}
					<p class="padding">No result found</p>
				{/if}
			</div>
		{/if}

	</div>
</main>
<footer>
	<p>Made with <a href="https://svelte.dev/" >Svelte.js</a> <img width="25px" src="https://th.bing.com/th/id/R.02f9ec2d33cc2727b182b07e53a35773?rik=sB8nh4ElbxLn7g&pid=ImgRaw&r=0" alt=""> by <a href="https://emmanueloladosu.com/">Emmanuel Oladosu</a></p>
  </footer>
  