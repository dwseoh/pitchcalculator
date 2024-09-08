<svelte:head>
	<title>Speedgun Online</title>
	<meta charset="utf-8" />
	<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no"/>
	<link href="https://fonts.googleapis.com/css2?family=DM+Sans:ital,opsz,wght@0,9..40,100..1000;1,9..40,100..1000&display=swap" rel="stylesheet">
	<link rel="icon" type="image/png" href="speedgun.svg" sizes="32x32" />
	<link rel="icon" type="image/png" href="speedgun.svg" sizes="16x16" />
</svelte:head>



<script lang='ts'>
	let status='none' //recording recorded none
	let display='Start'
	let resultDisplay = ''
	let errorMessage = ''
	let distance = 18.39
	let unit = 'meters'
	let speed = 0.0
	let startTime = Date.now()
	let elapsedTime = 0
	let interval

	function calculate(){
		if (unit == 'meters'){
			speed = distance/(elapsedTime/1000)*3.6 //km/h
			resultDisplay = Math.round(speed)+'km/h'
		}
		else {
			speed = distance/(elapsedTime/1000)*3600/5280 //mph
			resultDisplay = Math.round(speed)+'mph'

		}

	}

	function checkStatus(){
		if (status == 'none' || status == 'recorded') {
			resetStopwatch()
			status = 'recording'
			display = 'Stop'
			startStopwatch()
			
		}
		else if (status == 'recording') {
			stopStopwatch()
			status = 'recorded'
			display = 'Start'
			calculate()
		}
	}

	
	function unitMeters(){
		unit = 'meters'
	}
	function unitFeet(){
		unit = 'feet'
	}

	function startStopwatch() {
		startTime = Date.now() - elapsedTime; 
		interval = setInterval(() => {
			elapsedTime = Date.now() - startTime;
		}, 1) 
	}

	function stopStopwatch() {
		clearInterval(interval)
	}

	function resetStopwatch() {
		clearInterval(interval)
		elapsedTime = 0
	}

	function formatTime(ms) {
		const seconds = Math.floor(ms / 1000);
		const milliseconds = ms%1000
		return `${seconds}.${milliseconds}`;
	}

	function showInstructions() {
		alert("INSTRUCTIONS\n1. Configure the distance, and choose your units (meters or feet)\n2. Press start as soon as the pitcher releases the ball from their hand\n3. Press stop as soon as the ball reaches the catcher's glove\n4. The resulting pitch would show in kmh or mph depending on your unit.")
	}

	
</script>

<div class='all'>

	<div class='top-section'>
		<img alt="thumbnail" id="thumbnail-image" src="speedgun.svg">
		<h1 id='thumbnail-title'>Speedgun<br> Online</h1>
	</div>

	<section class='main-section'>
		<div id='main-section-top'>
			<label id='distance-input-label'  for="distance-input-label">Distance:</label>
			<input bind:value={distance} type="number" id="distance-input"  name="distance-input-label">
			
			
		</div>
		<div id='main-section-middle'>
			<input type="radio" id="meter" name="unit" checked value="meter" on:click={unitMeters} >
			<label id='meter-label'for="meter">meters</label>
			<input on:click={unitFeet} type="radio" id="feet" name="unit" value="feet">
			<label id='feet-label' for="feet">feet</label>
			<p>{errorMessage}</p>
		</div>
		<div id='main-section-bottom'>
			<button class={status==='recording' ? 'event-button-pressed' : 'event-button'} on:click={checkStatus}>
				{display}
			</button>
		</div>
		<p>{formatTime(elapsedTime)}</p>
	</section>

	<section class='results'>
	
		<p id='result-text'>{resultDisplay}</p>
	</section>

	<footer>
		<p on:click={showInstructions} class='footer-element link'>Instructions</p>
		<p class='footer-element'><a class='link' href='https://dwseoh.com' target='_blank'>dwseoh.com</a></p>
	</footer>

</div>


<style>


	@import url('https://fonts.googleapis.com/css2?family=DM+Sans:ital,opsz,wght@0,9..40,100..1000;1,9..40,100..1000&display=swap');	
	
	.all{
		font-family: 'DM Sans';
		color: rgb(209, 208, 208);
		margin:0;
		overflow:hidden;
	}

	footer{
		display:flex;
		bottom:0;
		position:relative;
		width:99vw;
		justify-content: center;
		overflow:hidden;
	}
	
	.footer-element{
		margin:0em 1.2em 2em 1.2em;
		font-size:1.2em;

	}

	.link,.link:active,.link:visited,.link:hover{
		color:rgb(209, 208, 208);
		text-decoration: none;
	}

	.link:hover{
		text-decoration: underline;
		cursor:pointer;
	}

	#result-text{
		text-align: center;
		font-size:2.5em;
		font-weight:500;
		color:#F2A30B;
		margin:0;
	}

	.results{
		margin:0em 0em 2em 0em;
	}

	.event-button-pressed{
		font-family: 'DM Sans';
		border:none;
		border-radius:5px;
		font-size:2em;
		margin: 0.5em 0em 0em 0em;
		padding: 0.5em 4em 0.5em 4em;
		background-color: #F2A30B;
		
	}

	.event-button{
		font-family: 'DM Sans';
		border:none;
		border-radius:5px;
		font-size:2em;
		margin: 0.5em 0em 0em 0em;
		padding: 0.5em 4em 0.5em 4em;
		background-color: rgb(209, 208, 208);
		will-change: contents;
		
	}

	#distance-input{
		margin:0em 1em 0em 1em;
		height:1.7em;
		padding-left:0.5em;
		width:4em;
		font-family: 'DM Sans';
		font-size:0.5em;
		border-radius:20px;
	}

	#thumbnail-title {
		font-size: 5em;
        text-align: center;
		line-height: 100px;
	}

	#meter{
		margin:0em 0.5em 0em 0.5em;
	}
	
	#feet{
		margin:0em 0.5em 0em 0.5em;
	}

	#meter-label{
		margin-right:0.5em;
	}

	#main-section-top{
		display:flex;
		font-size:3em;
		font-weight:500;
		align-items: center;
	}

	#main-section-bottom{
		display:flex;
	}

	#main-section-middle{
		display:flex;
		align-items: center;
		font-size:1.4em;
		justify-content: flex-end; 

	}
	

	#thumbnail-image{
		width:15%;
		margin-right:2em;
	}

	.main-section{
		display:flex;
		flex-direction: column;
		align-items: center;
	
	}

	.top-section{
		display:flex;
		justify-content: center;
		margin:2.5em 0em 1em 0em;
		padding-right:7em;
	}


	
	@media screen and (max-width:700px)  {
		#thumbnail-title{
			font-size:4em;
			line-height:80px;
		}

		#thumbnail-image{
			margin-right:1.5em;
			width:25%;
		}

		.event-button,.event-button-pressed{
			font-size:1.95em;
		}

		#distance-input{
			font-size:0.48em;
		}

		#main-section-top{
			font-size:2.8em;
		}

		#main-section-middle{
			font-size:1.3em;
		}



	}

	@media screen and (max-width:570px)  {

		.top-section{
			flex-direction: column;
			align-items: center;
			width:100vw;
			padding-right:0em;
			margin:1.8em 0em 1em 0em;

		}

		#thumbnail-image{
			margin: 0em 0em 0em 0em;
			width:35%;
			justify-self: center;
		}

		#thumbnail-title{
			font-size:4em;
			line-height:80px;
			margin: 0.1em 0em 0.1em 0em;
		}

		.event-button,.event-button-pressed{
			font-size:1.65em;
		}

		#distance-input{
			font-size:0.45em;
		}

		#main-section-top{
			font-size:2.5em;
		}

		#main-section-middle{
			font-size:1.1em;
		}

	}



</style>