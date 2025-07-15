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
			<img class="the-man" src="https://trainerday.com/wp-content/uploads/2023/09/home.jpeg" alt="background">
			<div class="body-container" id="content">
			<h1>Cycling Calculators</h1>
				<div class="calc">
					<Power_to_speed />
				</div> 
			</div>
		</main>
		<footer>
			We're really cool
		</footer>
	</div>
</template>

<style scoped>
	.app-layout {
		display: block;
		flex-direction: column;
		min-height: 100vh;
	}

	.main-content {
		display: inline-block;
		min-width: 100vw;
		max-width: 100%;
		min-height: fit-content;
		overflow: visible;
	}

	main img {
		position: absolute;
		right: 0;
		width: 100%;
		height: auto;
		/* display: block; */
		object-fit: contain;
		z-index: -1;
		pointer-events: none;
	}

	.body-container {
		position: relative;
		display: flex;
		/* display: none; */
		flex-direction: column;
		/* size; */
		padding-right: 30%;
		padding-left: 5%;
		margin-bottom: 30px;
	}

	.calc {
		background-color: var(--secondary);
		
		border: rgba(128, 128, 128, 100) 5px solid;
		height: 100%;
		border-radius: 1.25%;
		color: black;
		z-index: 2;
	}

	h1 {
		display: inline;
		text-align: center;
		color: var(--secondary);
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

	@media (max-width: 1200px) {
        .app-layout {
			background-color: var(--tertiary);
		}

		.main-content {
			display: flex;
			overflow: visible;
			position: static;
			min-height: fit-content;
			align-items: center;
			justify-content: center;
		}
		
		.body-container {
			display: block;
			position: static;
			max-width: 95%;
			padding: 0;
			margin-top: 12px;
		}

		h1 {
			display: none;
		}

		main > img {
			display: none;
			object-fit: unset;
		}
    }
</style>
