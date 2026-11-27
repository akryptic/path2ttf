<script lang="ts">
	import './layout.css';
	import type { LayoutProps } from './$types';

	let { children }: LayoutProps = $props();
</script>

<svelte:head>
	<link rel="icon" href="/favicon.svg" />
	<meta name="theme-color" content="#1b1e24" />
	<meta name="color-scheme" content="dark" />
	<meta property="og:site_name" content="path2ttf" />
	<meta property="og:type" content="website" />
</svelte:head>

{@render children()}
