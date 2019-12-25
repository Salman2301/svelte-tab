<script>
	import {onDestroy} from "svelte";
	
	export let id;
	
	onDestroy(()=>{
		console.log("destroied : " , id);
	})
</script>

<p>
	THIS IS AN SAMPLE TAB ID: {id}
</p>

<input value="sad"/>