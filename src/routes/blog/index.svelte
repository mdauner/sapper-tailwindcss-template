<script context="module">
	export function preload({ params, query }) {
		return this.fetch(`blog.json`).then(r => r.json()).then(posts => {
			return { posts };
		});
	}
</script>

<script>
	export let posts;
</script>

<svelte:head>
	<title>Blog</title>
</svelte:head>

<div class="text-3xl font-bold mb-2">Recent posts</div>

<ul class="mb-4">
	{#each posts as post}
		<!-- we're using the non-standard `rel=prefetch` attribute to
				tell Sapper to load the data for the page as soon as
				the user hovers over the link or taps it, instead of
				waiting for the 'click' event -->
		<li class="list-disc list-inside">
			<a
				class="hover:underline hover:text-blue-500"
				rel="prefetch"
				href="blog/{post.slug}">
        		{post.title}
      		</a>
    	</li>
	{/each}
</ul>