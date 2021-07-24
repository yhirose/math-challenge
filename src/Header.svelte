<script>
</script>

<main>
    <div class="content">
        <slot></slot>
    </div>
</main>

<style>
    main {
        padding: 4px;
    }

    .content {
        display: flex;
        justify-content: space-between;
        height: 48px;
        padding: 0 16px;
        border-bottom: 1px solid lightgray;
    }
</style>