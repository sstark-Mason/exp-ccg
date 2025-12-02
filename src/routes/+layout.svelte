<script lang="ts">
	import "./app.css";
	import debug from "debug";
	const log = debug("app:layout");
	localStorage.debug = "app:*";
	import { PersistedState } from "runed";
	import { onMount } from "svelte";
	import { InstructionsProgress } from "$lib/InstructionsProgress";

	onMount(() => {
		const colorTheme = localStorage.getItem("color-theme") || "light";
		document.documentElement.classList.add(colorTheme);
	});	

	let { children } = $props();
</script>

<svelte:head>
</svelte:head>

<div class="layout-grid">
    <aside class="sidebar left-sidebar">
        <ul class="panel-list"><span class="instructions-label">Instructions</span>
            <li><a href="/instructions/welcome" class="panel-button">Welcome</a></li>
			<li><a href="/instructions/overview" class="panel-button">Overview</a></li>
			<li><a href="/instructions/game" class="panel-button">Game</a></li>
            <!-- Add left sidebar content -->
        </ul>
    </aside>
    
    <main class="content">
        {@render children()}
    </main>
    
    <aside class="sidebar right-sidebar">
    	<ul class="panel-list">
			<span class="instructions-label">Stuff</span>
			<li><a href="" class="panel-button">Settings</a></li>
		</ul>
    </aside>
</div>

<style>
	:global(body) {
		margin: 0;
		padding: 0;
	}

    .layout-grid {
        display: grid;
        grid-template-columns: 200px 1fr 200px; /* Adjust widths as needed */
        min-height: 100vh;
    }
    
    .sidebar {
        background: #000000bb;
    }

	.panel-list {
		list-style: none;
		padding: 0;
		margin: 0;
	}

	.instructions-label {
		display: block;
		padding: 1rem;
		font-weight: bold;
		color: white;
		background: #333;
		text-align: center;
		margin-bottom: 0.5rem;
	}

	.panel-button {
        display: block;
        width: 100%;
        padding: 0.75rem 1rem;
        /* margin-bottom: 0.5rem; */
        background: #007bff;
        color: white;
		font-weight: bold;
		font-size: 1rem;
        text-decoration: none;
        border: none;
        text-align: center;
        transition: background 0.3s;
		box-sizing: border-box;
    }

	.panel-button:hover {
        background: #0056b3;
    }
    
    .content {
        padding: 1rem;
    }
    
    /* Responsive: Stack on small screens */
    @media (max-width: 768px) {
        .layout-grid {
            grid-template-columns: 1fr;
        }
        .left-sidebar, .right-sidebar {
            display: none; /* Or toggle via JS */
        }
    }
</style>
