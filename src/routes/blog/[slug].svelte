<script context="module">
	export async function preload({ params, query }) {
		// the `slug` parameter is available because
		// this file is called [slug].svelte
		const res = await this.fetch(`blog/${params.slug}.json`);
		const data = await res.json();

		if (res.status === 200) {
			return { post: data };
		} else {
			this.error(res.status, data.message);
		}
	}
</script>

<script>
	export let post;
</script>

<style>
	/*
		By default, CSS is locally scoped to the component,
		and any unused styles are dead-code-eliminated.
		In this page, Svelte can't know which elements are
		going to appear inside the {{{post.html}}} block,
		so we have to use the :global(...) modifier to target
		all elements inside .content
	*/
	.content :global(h2) {
    	@apply text-2xl font-bold;
	}

	.content :global(pre) {
    	@apply bg-gray-100 shadow p-2 rounded overflow-x-auto;
	}

	.content :global(pre) :global(code) {
		@apply bg-transparent p-0;
	}

	.content :global(ul) {
		@apply leading-normal;
	}

	.content :global(li) {
		@apply mb-2;
	}
</style>

<svelte:head>
	<title>{post.title}</title>
</svelte:head>

<div class="text-3xl font-bold mb-2">{post.title}</div>

<div class="content">
	{@html post.html}
</div>
