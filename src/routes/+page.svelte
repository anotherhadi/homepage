<script lang="ts">
	import Button from '$lib/components/ui/button/button.svelte';
	import { Separator } from '$lib/components/ui/separator';
	import { config } from './config.json';

	let date = new Date().toLocaleDateString(config.locale);
	let time = new Date().toLocaleTimeString(config.locale);

	let title = config.title;
	let openOnNewTab = config.openLinksInNewTab;
	let folders = config.folders;
</script>

<svelte:head>
	<title>{title}</title>
</svelte:head>

<header class="mb-2 mt-10 flex flex-col gap-4">
	<div class="flex w-full flex-wrap items-center justify-between">
		<p class="max-w-xl text-sm font-medium leading-none" style="color: {config.colors.muted}">
			{date}
		</p>
		<p class="max-w-xl text-sm font-medium leading-none" style="color: {config.colors.muted}">
			{time}
		</p>
	</div>

	<h1
		class="my-2 scroll-m-20 text-4xl font-extrabold tracking-tight lg:text-5xl"
		style="color: {config.colors.primary}"
	>
		{title}
	</h1>
	<Separator class="my-4" style="background: {config.colors.muted};" />
</header>

<div class="w-full" style="color: {config.colors.foreground}">
	{#each folders as folder}
		<h2 class="my-4 whitespace-pre font-['NerdFont'] text-2xl font-bold">{folder.name}</h2>
		<div class="mb-9 grid grid-cols-1 gap-2 md:grid-cols-2 lg:grid-cols-3">
			{#each folder.links as link}
				<a href={link.url} target={openOnNewTab ? '_blank' : '_self'} rel="noopener noreferrer">
					<Button variant="ghost" size="lg" class="flex w-full items-center gap-5 p-5 py-10">
						<div class="w-16 overflow-hidden">
							<span class="font-['NerdFont'] text-4xl">{link.icon}</span>
						</div>
						<div class="relative flex w-full flex-col gap-2 overflow-hidden text-left">
							<p class="text-lg font-medium leading-none">
								{link.title}
							</p>
							<p
								class="overflow-hidden overflow-ellipsis whitespace-nowrap text-sm font-medium leading-none"
								style="color: {config.colors.muted}"
							>
								{link.url}
							</p>
						</div>
					</Button>
				</a>
			{/each}
		</div>
	{/each}
</div>
