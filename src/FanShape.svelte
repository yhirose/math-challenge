<script>
    export let degree = 0;
    export let fill = '#000';
    export let invert = false;

    $: x = 0 + 50 * Math.sin(degree / 180 * Math.PI);
    $: y = 0 - 50 * Math.cos(degree / 180 * Math.PI);
    $: sf = invert ? (degree < 180 ? 1 : 0) : (degree > 180 ? 1 : 0);
</script>

 <svg viewBox="-50 -50 100 100" style="--fill: {fill}">
    {#if invert}
        {#if degree === 0}
            <circle class="face" cx="0" cy="0" r="50" />
        {:else}
            <path class="face" d="M 0 0 L {x} {y} A 50 50 0 {sf} 1 0 -50 Z" />
        {/if}
    {:else}
        <path class="face" d="M 0 0 L 0 -50 A 50 50 0 {sf} 1 {x} {y} Z" />
    {/if}
</svg>

<style>
    svg {
        height: 100%;
        width: 100%;
    }

    .face {
        fill: var(--fill);
    }
</style>