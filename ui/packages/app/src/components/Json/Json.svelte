<script lang="ts">
	import { createEventDispatcher } from "svelte";
	import { JSON } from "@gradio/json";
	import { Block, BlockLabel } from "@gradio/atoms";
	import { JSON as JSONIcon } from "@gradio/icons";

	import StatusTracker from "../StatusTracker/StatusTracker.svelte";
	import type { LoadingStatus } from "../StatusTracker/types";
	import type { Styles } from "@gradio/utils";
	import { _ } from "svelte-i18n";

	export let elem_id: string = "";
	export let visible: boolean = true;
	export let value: any;
	export let loading_status: LoadingStatus;
	export let label: string;
	export let style: Styles = {};

	const dispatch = createEventDispatcher<{ change: undefined }>();

	$: value, dispatch("change");
</script>

<Block
	{visible}
	test_id="json"
	{elem_id}
	disable={typeof style.container === "boolean" && !style.container}
>
	{#if label}
		<BlockLabel
			Icon={JSONIcon}
			{label}
			disable={typeof style.container === "boolean" && !style.container}
		/>
	{/if}

	<StatusTracker {...loading_status} />

	<JSON {value} copy_to_clipboard={$_("interface.copy_to_clipboard")} />
</Block>
