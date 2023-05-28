<script lang="ts">
	import { Accordion, AccordionItem } from '$lib/components/accordion';

	const content =
		'Lorem ipsum dolor sit amet consectetur, adipisicing elit. Ex ea illo fuga repellat quisquam magni hic corporis, ratione totam cupiditate ipsam, odit, tempore nobis aperiam officiis alias explicabo asperiores maiores.';

	const items = [
		{ title: 'Accordion 1', content },
		{ title: 'Accordion 2', content },
		{ title: 'Accordion 3', content },
		{ title: 'Accordion 4', content },
		{ title: 'Accordion 5', content }
	];
</script>

<section>
	<Accordion 
        --accordion-width="70ch" 
        --accordion-background="#ccc"
        --accordion-color="#000"
        >
		{#each items as item}
			<AccordionItem>
				<svelte:fragment slot="title">{item['title']}</svelte:fragment>
				<svelte:fragment slot="content">{item['content']}</svelte:fragment>
			</AccordionItem>
		{/each}
	</Accordion>
</section>
