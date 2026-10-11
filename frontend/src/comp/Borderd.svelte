<script lang="ts">
	let { children, className = "", ...rest} = $props();
</script>

<div class={`border border-white p-1 ${className}`} {...rest}>
    {@render children?.()}
</div>
