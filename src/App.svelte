<script>
	let results = '';
	let errors = '';
	let flipRun = '';
	function handleSearch(query) {
			fetch(`https://dictionaryapi.com/api/v3/references/thesaurus/json/${query}?key=c076686b-3d9f-4302-a9db-c083c1f7422e`)
		.then(response => response.json())
		.then(data => {results = data[0].meta.syns[0]; errors = ''})
		.catch(error => errors = 'No synonyms availible')
	}

	function flip(event) {

		if (flipRun === 'flip-in-ver-right') {
			flipRun = 'flip-in-ver-left'
			return
		}

		if (event.target.classList.contains("word"))
		{
		flipRun = "flip-in-ver-right"
		return
		}
	}

	function checkFlip(event) {

	}
</script>

<style>


p {
	display: flex;
	justify-content: space-evenly;
	flex-flow: wrap;
}

span {
 background-color: #b82dff;
 margin: 10px;
 padding: 10px;
 border-radius: 5px;
 color: white;
 font-weight: bold;
}

span:hover {
	cursor: pointer;
	background-color: #fb961a;
	box-shadow: 3px 3px 8px 0px black;
}

input {
	text-align: center;
}

section {
	text-align: center;
	margin-left: auto;
	margin-right: auto;
	font-size: 20px;
	font-weight: bold;
}

.flip-in-ver-right {
	-webkit-animation: flip-in-ver-right 0.7s cubic-bezier(0.250, 0.460, 0.450, 0.940) both;
	        animation: flip-in-ver-right 0.7s cubic-bezier(0.250, 0.460, 0.450, 0.940) both;
}

.flip-in-ver-left {
	-webkit-animation: flip-in-ver-left 0.7s cubic-bezier(0.250, 0.460, 0.450, 0.940) both;
	        animation: flip-in-ver-left 0.7s cubic-bezier(0.250, 0.460, 0.450, 0.940) both;
}

@-webkit-keyframes flip-in-ver-right {
  0% {
    -webkit-transform: rotateY(-80deg);
            transform: rotateY(-80deg);
    opacity: 0;
  }
  100% {
    -webkit-transform: rotateY(0);
            transform: rotateY(0);
    opacity: 1;
  }
}
@keyframes flip-in-ver-right {
  0% {
    -webkit-transform: rotateY(-80deg);
            transform: rotateY(-80deg);
    opacity: 0;
  }
  100% {
    -webkit-transform: rotateY(0);
            transform: rotateY(0);
    opacity: 1;
  }
}

@-webkit-keyframes flip-in-ver-left {
  0% {
    -webkit-transform: rotateY(80deg);
            transform: rotateY(80deg);
    opacity: 0;
  }
  100% {
    -webkit-transform: rotateY(0);
            transform: rotateY(0);
    opacity: 1;
  }
}
@keyframes flip-in-ver-left {
  0% {
    -webkit-transform: rotateY(80deg);
            transform: rotateY(80deg);
    opacity: 0;
  }
  100% {
    -webkit-transform: rotateY(0);
            transform: rotateY(0);
    opacity: 1;
  }
}

</style>

<section>
	SYNONYM FINDER <br/>
	<input on:keyup={event => handleSearch(event.target.value)} placeholder="Search">
</section>
<p>{errors}</p>
<p on:click={async (event) => {await checkFlip(event); flip(event);}} class={flipRun}>
	{#each results as result, i}
    <span class="word" on:click={event =>  handleSearch(event.target.innerHTML)}>{result.toUpperCase()}</span>
{/each}
</p>
