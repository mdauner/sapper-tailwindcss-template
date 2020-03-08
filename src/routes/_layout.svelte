<script>
	import Nav from '../components/Nav.svelte';

	export let segment;
</script>

<Nav {segment}/>

<main class="relative max-w-3xl bg-white p-8 mx-auto">
	<slot></slot>
</main>