<script>
    import Keyboard from "./Keyboard.svelte";

    export let onCategory;
    export let onAccount;
    export let onValueChanged = () => {};
    export let onSubmit = () => {};
    export let inputs = [0];

    let hasComma = false;

    const buttons = [
        {},
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
        {
            value: ",",
            id: "btn-comma",
            action: onComma,
        },
        {
            value: "=",
            id: "btn-enter",
            action: onEnter,
        },
    ];

    const btnIds = [0, 1, 2, 4, 5, 6, 8, 9, 10, 12];
    for (let i = 9; i >= 0; i--) {
        buttons[btnIds[9 - i]] = {
            value: i,
            id: `num-${i}`,
            action: onNumber,
        };
    }

    function onNumber(ev) {
        let num = parseInt(ev.target.innerText);
        if (inputs[0] === 0 && inputs.length == 1) {
            inputs[0] = num;
        } else {
            inputs.push(num);
        }
        onValueChanged(inputs);
    }
    function onComma(ev) {
        if (hasComma) return;
        hasComma = true;
        inputs.push(",");
        onValueChanged(inputs);
    }
    function onClear(ev) {
        inputs = [0];
        hasComma = false;
        onValueChanged(inputs);
    }
    function onEnter(ev) {
        let total = 0;
        let commatAt = inputs.length;
        for (let i = 0; i < inputs.length; i++) {
            if (inputs[i] === ",") {
                commatAt = i + 1;
                continue;
            }
            total = total * 10 + inputs[i];
        }
        // 0,123 == 123/10**3
        // 3 = 5 - 1 - 1
        // 123,4356 = /10**4
        // 4 = 8 - 1 - 3

        total = total / Math.pow(10, inputs.length - commatAt);

        console.log(total);
        onSubmit(total);
    }
</script>

<Keyboard {buttons} />

<style>
</style>
