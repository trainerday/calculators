<script setup>
import Power_to_speed from './components/power_to_speed.vue';
import img_link from './components/img_link.vue';


</script>

<template>
	<div class="app-layout">
		<header>
			<div class="header" id="content">
				<div>
					<img_link 
						img="https://trainerday.com/wp-content/uploads/2023/09/td_white.svg"
						link="https://trainerday.com/"
						:size="{
							width: 171,
							height: 39,
						}"
					/>
				</div>
			</div>
		</header>
		<main class="main-content">
			<img src="https://trainerday.com/wp-content/uploads/2023/09/home.jpeg" alt="background">
		</main>
		<div class="body-container" id="content">
			<h1>Cycling Calculators</h1>
			<div class="calc">
				<Power_to_speed />
			</div> 
		</div>
		<footer>
			We're really cool
		</footer>
	</div>
</template>

<style scoped>
	#content {
		max-width: 68%;
	}

	.app-layout {
		display: block;
		flex-direction: column;
		min-height: 100vh;
	}

	.main-content {
		position: relative;
		display: inline-block;
		min-width: 100vw;
		max-width: 100%;
		overflow: hidden;
	}

	.main-content img {
		width: 100%;
		height: auto;
		display: block;
		object-fit: contain;
		z-index: -1;
		pointer-events: none;
	}

	.body-container {
		position: absolute;
		display: flex;
		flex-direction: column;
		top: 7%;
		left: 5%;
		right: 50%;
	}

	.calc {
		background-color: white;
		border: grey 5px solid;
		height: 100%;
		border-radius: 1%;
		color: black;
		z-index: 2;
	}

	h1 {
		display: inline;
		text-align: center;
		text-justify: center;
		color: white;
	}

	header {
		display: flex;
		background: var(--primary);
		justify-content: center;
		align-items: center;
	}

	.header {
		padding: 16px 10px 16px 10px;
		height: 39px;
		display: flex;
		
		flex-direction: row;
	}

	footer {
		display: block;
		background-color: #333;
		color: white;
		padding: 1
	}
</style>
