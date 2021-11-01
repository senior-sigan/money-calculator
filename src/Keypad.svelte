<script>
    import Keyboard from "./Keyboard.svelte";

    export let onCategory;
    export let onAccount;
    export let onSelected;
    export let buttons = [];

    const keypad = [
        {
            value: "any",
            action: onSelect,
        },
        {},
        {},
        {
            value: "AC",
            id: "btn-clear",
            action: onClear,
        },
        {},
        {},
        {},
        {
            value: "acc",
            id: "btn-account",
            action: onAccount,
        },
        {},
        {},
        {},
        {
            value: "cat",
            id: "btn-category",
            action: onCategory,
        },
        {},
        {},
        {},
    ];

    const btnIds = [1, 2, 4, 5, 6, 8, 9, 10, 12, 13, 14];
    for (let i = 0; i < btnIds.length; i++) {
        let button = buttons[i];
        let btn = {
            value: "",
            id: "",
            action: undefined,
        };
        if (button) {
            btn.value = button.icon;
            btn.action = onSelect;
        }
        keypad[btnIds[i]] = btn;
    }

    function onSelect(ev) {
        onSelected("any");
    }
    function onClear(ev) {}
</script>

<Keyboard buttons={keypad} />

<style>
</style>
