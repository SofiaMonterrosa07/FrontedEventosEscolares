<script>
	import favicon from "../lib/assets/favicon.svg";
	import Header from "../lib/components/Header.svelte";
	import Navbar from "../lib/components/Navbar.svelte";
	import Footer from "../lib/components/Footer.svelte";
	import 'bootstrap-icons/font/bootstrap-icons.css';
	import { page } from '$app/state';

	let { children } = $props();
</script>

<svelte:head>
	<link rel="icon" href={favicon} />

	<meta
		name="viewport"
		content="width=device-width, initial-scale=1"
	/>

	<title>Gestión de Eventos Escolares</title>
</svelte:head>

{#if page.url.pathname === '/'}
	{@render children()}
{:else}
	<Header></Header>

	<Navbar></Navbar>

	<main class="min-vh-100 bg-light">
		{@render children()}
	</main>

	<Footer></Footer>
{/if}