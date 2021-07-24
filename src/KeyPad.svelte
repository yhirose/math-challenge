<script>
    import { createEventDispatcher } from 'svelte';
    const dispatcher = createEventDispatcher();
    function handleClick(event) {
        const { key } = event.target.dataset;
        if (key) {
            dispatcher('key', { key })
        }
    }
</script>

<main on:click={handleClick}>
    <div class="key no-left" data-key="1" >1</div>
    <div class="key" data-key="2" >2</div>
    <div class="key" data-key="3" >3</div>
    <div class="key no-left" data-key="4" >4</div>
    <div class="key" data-key="5" >5</div>
    <div class="key" data-key="6" >6</div>
    <div class="key no-left" data-key="7" >7</div>
    <div class="key" data-key="8" >8</div>
    <div class="key" data-key="9" >9</div>
    <div class="key no-left" data-key="clr" >C</div>
    <div class="key" data-key="0" >0</div>
    <div class="key" data-key="bs" >←</div>
</main>

<style>
	main {
        height: 240px;
        display: grid;
        grid-template-columns: 1fr 1fr 1fr;
        grid-template-rows: 1fr 1fr 1fr 1fr;
        padding: 4px;
	}

    .key {
        display: grid;
        place-items: center;
        font-size: 18pt;
        cursor: pointer;
		border-top: 1px solid lightgrey;
		border-left: 1px solid lightgrey;
    }

    .key.no-left {
		border-left: 0;
    }
</style>