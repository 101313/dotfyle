<script lang="ts">
	import type { JsonBreakingChangePost } from '$lib/types';
	import { humanizeAbsolute } from '$lib/utils';
	import { faGithub } from '@fortawesome/free-brands-svg-icons';
	import { faChevronCircleRight } from '@fortawesome/free-solid-svg-icons';
	import Fa from 'svelte-fa';
	import CoolText from './CoolText.svelte';
	import CoolTextOnHover from './CoolTextOnHover.svelte';

	export let post: JsonBreakingChangePost;

	const date = new Date(post.createdAt);
	const url = `/plugins/${post.breakingChange.plugin.owner}/${post.breakingChange.plugin.name}`;
	const title = `Breaking change in ${post.breakingChange.plugin.name}`;
	const text = post.title;
	const githubLink = post.breakingChange.externalUrl;
	const shortSha = post.breakingChange.sha.substring(0, 6);
</script>

<div
	class="relative flex flex-col justify-between overflow-hidden rounded-md bg-white/10 transition-colors w-full hover:bg-white/20"
>
	<div class="flex items-center space-x-2 pt-2 py-1 pl-5">
		<CoolTextOnHover>
			<a class="flex gap-2 items-center" href={url}>
				<div class="text-sm font-semibold tracking-wide">
					{title}
				</div>
				<Fa class="force-white-text" size="sm" icon={faChevronCircleRight} />
			</a>
		</CoolTextOnHover>
	</div>
	<div class="flex items-center space-x-2 pl-5">
		<div class="flex gap-2 text-sm font-normal tracking-wide">
			<a class="flex gap-1 w-auto items-center" href={githubLink} target="_blank">
				<Fa size="sm" icon={faGithub} />
				<CoolText text={shortSha} />
			</a>
			{humanizeAbsolute(date)}
		</div>
	</div>
	<div class="flex items-center space-x-2 p-2 pl-5 h-full">
		<span class="text-sm font-normal tracking-wide flex gap-2">
			{text}
		</span>
	</div>
</div>
