# Svelte Tab
## Demo
[click here](https://svelte.dev/repl/6e82b757c2354437920f0c9679773c1d?version=3.16.7)

## How to use
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
