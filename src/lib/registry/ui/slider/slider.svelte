<script lang="ts">
	import { Slider as SliderPrimitive } from "bits-ui";
	import { cn, type WithoutChildrenOrChild } from "#lib/utils.js";

	let {
		ref = $bindable(null),
		value = $bindable(),
		orientation = "horizontal",
		class: className,
		...restProps
	}: WithoutChildrenOrChild<SliderPrimitive.RootProps> = $props();
</script>

<!--
Discriminated Unions + Destructing (required for bindable) do not
get along, so we shut typescript up by casting `value` to `never`.
-->
<SliderPrimitive.Root
	bind:ref
	bind:value={value as never}
	data-slot="slider"
	{orientation}
	class={cn(
		"data-vertical:min-h-40 relative flex w-full touch-none items-center select-none data-disabled:opacity-50 data-vertical:h-full data-vertical:w-auto data-vertical:flex-col",
		className
	)}
	{...restProps}
>
	{#snippet children({ thumbItems })}
		<span
			data-slot="slider-track"
			data-orientation={orientation}
			class={cn(
				"border bg-muted rounded-full data-horizontal:h-3 data-horizontal:w-full data-vertical:h-full data-vertical:w-3 bg-muted relative grow overflow-hidden data-horizontal:w-full data-vertical:h-full"
			)}
		>
			<SliderPrimitive.Range
				data-slot="slider-range"
				class={cn(
					"bg-primary absolute select-none data-horizontal:h-full data-vertical:w-full"
				)}
			/>
		</span>
		{#each thumbItems as thumb (thumb.index)}
			<SliderPrimitive.Thumb
				data-slot="slider-thumb"
				index={thumb.index}
				class="border-ring ring-ring/50 relative size-5 rounded-full border bg-white transition-[color,box-shadow] after:absolute after:-inset-2 hover:ring focus-visible:ring-ring focus-visible:ring-offset-2 focus-visible:ring focus-visible:outline-hidden active:ring block shrink-0 select-none disabled:pointer-events-none disabled:opacity-50"
				aria-label={`Thumb ${thumb.index + 1}`}
			/>
		{/each}
	{/snippet}
</SliderPrimitive.Root>
