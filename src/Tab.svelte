<script>
	import {onMount} from "svelte";
	
	export let component;
	export let label;
	let currTab;
	
	export let tabs = [];
	
	let genRanID = function () {
  	return '_' + Math.random().toString(36).substr(2, 9);
	}
	
	onMount(()=>{
		
		// init
		let id = genRanID();
		currTab = id;
		tabs = [{
			id: id,
			component : component
		}];
	});
	
	
	
	const handleAddClick = e =>{
		let newID = genRanID(); 
		tabs = [...tabs,{
			id: newID,
			component : component
		}];
		currTab= newID;
	}
	const handleDelClick = id => {
		if(tabs.length===1) {
			console.log("one tab left, can't delete");
			return;
		}
		if(currTab === id) {
			// current tab is deleted, go back to previous tab
			let ids = tabs.map(el=>el.id);
			let pos = ids.indexOf(id);
			currTab = tabs[pos-1].id;
		}
		tabs = tabs.filter((el)=>el.id!==id);
		
	}
	
</script>

<div class="tab-header">
	{#each tabs as tab, i}
		<div class="btn-tab" class:selected={tab.id===currTab} on:click={()=>{currTab=tab.id}}>
			<p class="btn-tab-label">
				{label} {i+1}
			</p>
			<button class="btn-tab-del" on:click={()=>{handleDelClick(tab.id)}}>x</button>
		</div>
	{/each}
		<div class="btn-tab-add" on:click={()=>{handleAddClick()}}>
			<button class="btn-tab add">+</button>
		</div>
</div>

{#each tabs as tab}
<div class="tabs" class:selected={tab.id===currTab}>
	<svelte:component this={component} id={tab.id}/>
</div>
{/each}

<style>
	.tab-header {
		display: flex;
		width: 100%;
		height: 30px;
		background-color: #ccc;
		position: absolute;
	}
	.btn-tab{
		position: relative;
		background: #ccc;
		margin: 0px;
		padding: 0px ;
		width: 100px;
		display: flex;
		border-right: 1px solid darkgrey;

	}
	.btn-tab.selected {
		background-color:white;
		display: flex;
		border-top: 1px solid darkgrey;
	}
	.btn-tab:first-child.selected {
		border-left: 1px solid darkgrey;
	}
	.btn-tab:hover > .btn-tab-del,
	.btn-tab.selected > .btn-tab-del {
		display: flex;
	}
	.btn-tab-label{
			margin : 0px;
			width: 80%;
			padding-top:2px;
			justify-content:center;
			text-align:center;
			cursor:pointer;
	}
	.btn-tab-del{
			margin : 0px;
			padding: 0px;
			background: rgba(0,0,0,0);
			border-width: 0px;
			cursor: pointer;
			float: right;
			width: 20%;
			display: none;
			padding-bottom:4px;
	}
	.btn-tab-add > button{
			border-width: 0px;
			cursor: pointer;
			height: 100%;
			border-radius: 0px;
			width:30px;
			text-align:center;
			justify-content: center;
			font-weight:bold;
			padding-bottom: 2px;
	}
	.btn-tab-add > button:hover{
		background-color:white;
	}
	.tabs {
		display:none;
		position: relative;
		margin-top: 50px; 
	}
	.selected {
		display: block;
	}
	
</style>

