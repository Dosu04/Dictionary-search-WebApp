<script>
  import { each } from "svelte/internal";   
  export let wordData = null;
  function playAudio(src){
    let audio = new Audio(src);
    audio.play();

  }


</script>

<style>
	.word-data{
		font-size: 1.5rem;
	}
    	/* Audio styles */
	.audios {
		display: flex;
		flex-wrap: wrap;
		justify-content: space-between;
		margin-bottom: 1rem;
	}

	.auido {
		margin: 0.5rem;
	}

	p i.fa-play-circle {
		margin-left: 0.5rem;
		cursor: pointer;
		color: #007bff;
	}

	/* Meaning styles */
	.meaning {
		margin-bottom: 1rem;
	}

	.part-of-speech {
		font-weight: bold;
		margin-bottom: 0.5rem;
	}

	.definitions {
		margin-left: 1rem;
	}

	.definition {
		margin-bottom: 0.5rem;
	}

	.definition p:first-child {
		margin-bottom: 0.25rem;
		font-weight: bold;
	}

	.definition p:last-child {
		margin-bottom: 0;
		font-style: italic;
		color: #666;
	}

</style>

<div class="word-data">
    {#if wordData.phonetics}
        <div class="audios">
            {#each wordData.phonetics as data}
                <div class="auido">
                    <p>
                        {data.text}
                        <!-- svelte-ignore a11y-click-events-have-key-events -->
                        <i class="fa fa-play-circle" on:click={()=>playAudio(data.audio)}></i>
                    </p>
                </div>                
            {/each}
        </div>
    {/if}
    {#each wordData.meanings as meaning}
        <div class="meaning">
                <div class="part-of-speech">&bull; {meaning.partOfSpeech}</div>
                <div class="definitions">
                    {#each meaning.definitions as data}
                        <div class="definition">
                            <p>Definition: <b>{data.definition}</b> </p>
                            {#if data.example}
                                <p>Exmaple: <i>{data.example}</i> </p>
                            {/if}
                        </div>
                    {/each}
                </div>
        </div>
    {/each}
</div>
<br>
<br>
<br>
<br>
<br>
<br>