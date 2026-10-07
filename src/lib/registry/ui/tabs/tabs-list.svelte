<script lang="ts">
	import { Tabs as TabsPrimitive } from "bits-ui";
	import { cn } from "#lib/utils.js";

	let {
		ref = $bindable(null),
		class: className,
		...restProps
	}: TabsPrimitive.ListProps = $props();
</script>

<TabsPrimitive.List
	bind:ref
	data-slot="tabs-list"
	class={cn(
		"border inline-flex h-12 w-full items-center justify-center rounded-lg p-1.5",
		className
	)}
	{...restProps}
/>
