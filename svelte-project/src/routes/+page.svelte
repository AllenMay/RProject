
<h1>Welcome to SvelteKit</h1>
<p>Visit <a href="https://kit.svelte.dev">kit.svelte.dev</a> to read the documentation</p>

<script lang="ts">
    async function getItems() {
        const res = await fetch('https://testapi.io/api/ndenlinger/roveiq');
        const items = await res.json();

        // console.log('the items', items.data.css);

        if (res.ok) {
            return items;
        } else {
            throw new Error(items);
        }
    }
    
    $: allItemsPromise = getItems();
</script>

<div>
    {#await allItemsPromise then items}    
    <div>{items.data.kiosk.name}</div>
    <div>{items.data.screen.name}</div>
    {/await}    
</div>
<svelte:head>
    <style>
            {allItemsPromise.data.css};
    </style>
</svelte:head>