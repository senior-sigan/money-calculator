<script>
	import Keypad from "./Keypad.svelte";
	import Numpad from "./Numpad.svelte";

	let inputs = [0];
	let Component = Numpad;
	let properties = {};
	let category = "any";
	let account = "any";

	function onValueChanged(inputs_) {
		inputs = inputs_;
	}
	function onCategorySelected(categoryName) {
		category = categoryName;
		toNumpadState();
	}
	function onAccountSelected(accountName) {
		account = accountName;
		toNumpadState();
	}
	function onSubmit(value) {
		console.log(value, category, account);
		inputs = [0];
		toNumpadState();
	}
	function toCateogryState() {
		Component = Keypad;
		properties = {
			onSelected: onCategorySelected,
			buttons: [],
		};
	}
	function toAccountState() {
		Component = Keypad;
		properties = {
			onSelected: onAccountSelected,
			buttons: [],
		};
	}
	function toNumpadState() {
		Component = Numpad;
		properties = {
			inputs: inputs,
			onValueChanged: onValueChanged,
			onCategory: toCateogryState,
			onAccount: toAccountState,
			onSubmit: onSubmit,
		};
	}

	toNumpadState();
</script>

<main>
	<div class="display">{inputs.join("")}</div>
	<svelte:component this={Component} {...properties} />
</main>

<style>
	main {
		background-color: black;
		width: 290px;
		padding: 8px;
	}
	.display {
		padding: 8px;
		height: 64px;
		color: white;
		font-weight: 400;
		font-size: 52px;
		align-items: flex-end;
		display: flex;
		justify-content: end;
	}
</style>
