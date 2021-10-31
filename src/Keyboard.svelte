<script>
    export let handleResult;

    let inputs = [0];
    let hasComma = false;

    function onNumber(ev) {
        let num = parseInt(ev.target.innerText);
        if (inputs[0] === 0 && inputs.length == 1) {
            inputs[0] = num;
        } else {
            inputs.push(num);
        }

        inputs = inputs; // force state reload
    }
    function onComma(ev) {
        if (hasComma) return;
        hasComma = true;
        inputs.push(",");
        inputs = inputs;
    }
    function onClear(ev) {
        inputs = [0];
        hasComma = false;
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

        if (handleResult) handleResult(total);
    }
    function onCategory(ev) {}
    function onAccount(ev) {}

    let buttons = [
        {
            value: 7,
            id: "num-7",
            action: onNumber,
        },
        {
            value: 8,
            id: "num-8",
            action: onNumber,
        },
        {
            value: 9,
            id: "num-9",
            action: onNumber,
        },
        {
            value: "AC",
            id: "clear",
            action: onClear,
        },
        {
            value: 4,
            id: "num-4",
            action: onNumber,
        },
        {
            value: 5,
            id: "num-5",
            action: onNumber,
        },
        {
            value: 6,
            id: "num-6",
            action: onNumber,
        },
        {
            value: "acc",
            id: "account",
            action: onAccount,
        },
        {
            value: 1,
            id: "num-1",
            action: onNumber,
        },
        {
            value: 2,
            id: "num-2",
            action: onNumber,
        },
        {
            value: 3,
            id: "num-3",
            action: onNumber,
        },
        {
            value: "cat",
            id: "category",
            action: onCategory,
        },
        {
            value: 0,
            id: "num-0",
            action: onNumber,
        },
        {
            value: ",",
            id: "comma",
            action: onComma,
        },
        {
            value: "=",
            id: "enter",
            action: onEnter,
        },
    ];
</script>

<div class="keyboard">
    <div class="display">{inputs.join("")}</div>
    <div class="buttons">
        {#each buttons as button}
            <button id={button.id} on:click={button.action}
                >{button.value}</button
            >
        {/each}
    </div>
</div>

<style>
    .keyboard {
        background-color: black;
        width: 290px;
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
    .buttons {
        display: grid;
        grid-template-columns: 22% 22% 22% 22%;
        grid-auto-rows: max-content;
        grid-gap: 10px;
        padding: 8px;
        cursor: pointer;
        user-select: none;
    }

    button {
        color: white;
        height: 64px;
        font-weight: 600;
        font-size: 1.2em;
        cursor: pointer;
        margin: 0px;
        background-color: #444444;
        border-radius: 32px;
        border-width: 0px;
    }

    #num-0 {
        grid-column: 1 / span 2;
    }
</style>
