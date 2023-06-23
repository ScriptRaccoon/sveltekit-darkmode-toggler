<script lang="ts">
	import { onMount } from "svelte";

	import { THEMES } from "$lib/config";
	import Sun from "./Sun.svelte";

	let current_theme: string;

	onMount(() => {
		const saved_theme =
			document.documentElement.getAttribute("data-theme");
		if (
			saved_theme &&
			Object.values(THEMES).includes(saved_theme)
		) {
			current_theme = saved_theme;
			return;
		}

		const preference_is_dark = window.matchMedia(
			"(prefers-color-scheme: dark)"
		).matches;

		const theme = preference_is_dark ? THEMES.DARK : THEMES.LIGHT;
		set_theme(theme);
	});

	function set_theme(theme: string) {
		if (!Object.values(THEMES).includes(theme)) return;
		const one_year = 60 * 60 * 24 * 365;
		document.cookie = `theme=${theme}; max-age=${one_year}; path=/`;
		document.documentElement.setAttribute("data-theme", theme);
		current_theme = theme;
	}

	function toggle_theme(): void {
		const theme =
			current_theme === THEMES.LIGHT
				? THEMES.DARK
				: THEMES.LIGHT;
		set_theme(theme);
	}
</script>

<nav>
	<ul>
		<li>
			<a href="/">Home</a>
		</li>
		<li>
			<a href="/about">About</a>
		</li>
		<li>
			<button aria-label="toggle theme" on:click={toggle_theme}>
				<Sun />
			</button>
		</li>
	</ul>
</nav>

<style>
	nav {
		background-color: var(--nav-color);
		padding: 1rem;
		transition: background-color 250ms;
	}

	ul {
		list-style-type: none;
		display: flex;
		justify-content: center;
		align-items: center;
		gap: 1.5rem;
	}

	button {
		width: 1.5rem;
		height: 1.5rem;
	}
</style>
