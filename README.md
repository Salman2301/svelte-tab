# Svelte Tab
Copy the code in src `src/Tab.svelte` and create a component in your app and paste it and then to use the tab

import the tab component and your any component
and wrap the component like this

```
<Tab component={Component} label="Tab" />
```


Full Code

```
<script>
	import Tab from "./Tab.svelte";
	import Component from "./Sample.svelte";
</script>


<Tab component={Component} label="Tab" />
```