<script>
    export let opr1;
    export let opr2;
    export let ope;
    export let ans;

    $: opr1s = String(opr1).padStart(2, ' ');
    $: opr2s = String(opr2).padStart(2, ' ');
    $: anss = String(ans).padStart(3, ' ');
</script>

<div class="outer">
    <div class="cell opr1-2">{opr1s[0]}</div>
    <div class="cell opr1-1">{opr1s[1]}</div>
    <div class="cell opr2-2">{opr2s[0]}</div>
    <div class="cell opr2-1">{opr2s[1]}</div>
    <div class="cell ope">{ope}</div>
    <div class="cell ans ans-3">{anss[0]}</div>
    <div class="cell ans ans-2">{anss[1]}</div>
    <div class="cell ans ans-1">{anss[2]}</div>
</div>

<style>
	.outer {
        display: grid;
        grid-template-columns: 44px 44px 44px;
        grid-template-rows: 64px 76px 76px;
	}

    .cell {
        display: grid;
        place-items: center;
        font-size: 48pt;
    }

    .cell.ans {
        color: orangered;
    }

    .opr1-1 {
        grid-column: 3;
        grid-row: 1;
    }

    .opr1-2 {
        grid-column: 2;
        grid-row: 1;
    }

    .opr2-1 {
        grid-column: 3;
        grid-row: 2;
    }

    .opr2-2 {
        grid-column: 2;
        grid-row: 2;
    }

    .ope {
        grid-column: 1;
        grid-row: 2;
        font-size: 32pt;
    }

    .ans-1 {
        grid-column: 3;
        grid-row: 3;
		border-top: 1px solid lightslategray;
    }

    .ans-2 {
        grid-column: 2;
        grid-row: 3;
		border-top: 1px solid lightslategray;
    }

    .ans-3 {
        grid-column: 1;
        grid-row: 3;
		border-top: 1px solid lightslategray;
    }
</style>