
<script>
	let status='none' //recording recorded none
	let display='Start'
	let errorMessage = ''
	let distance = 18.39
	let unit = 'meters'
	function checkStatus(){
		if (status == 'none' || status == 'recorded') {
			status = 'recording'
			display = 'Stop'
			
		}
		else if (status == 'recording') {
			status = 'recorded'
			display = 'Start'
		}
	}

	function unitMeters(){
		unit = 'meters'
	}
	function unitFeet(){
		unit = 'feet'
	}

</script>

<div class='all'>
	<!-- <h1>Hello {name}!</h1> -->
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
	</section>

	<section class='results'>

	</section>

	<section class='instructions'>
		
	</section>

</div>
<!--  later use variables for device compatability in html -->


<style>
	.all{
		font-family: 'DM Sans';
		color: rgb(209, 208, 208);

	}

	.event-button-pressed{
		font-family: 'DM Sans';
		border:none;
		border-radius:5px;
		font-size:2em;
		margin: 0.5em 0em 0em 0em;
		padding: 0.1em 4em 0.1em 4em;
		background-color: #F2A30B;
		
	}

	.event-button{
		font-family: 'DM Sans';
		border:none;
		border-radius:5px;
		font-size:2em;
		margin: 0.5em 0em 0em 0em;
		padding: 0.1em 4em 0.1em 4em;
		background-color: rgb(209, 208, 208);
		
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
</style>