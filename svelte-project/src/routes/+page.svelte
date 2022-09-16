<script lang="ts">
    async function getItems() {
        const res = await fetch('https://testapi.io/api/ndenlinger/roveiq');
        const items = await res.json();

        if (res.ok) {
            return items;
        } else {
            throw new Error(items);
        }
    }    
    $: allItemsPromise = getItems();
</script>
<section class="globalHome">
    <div class="b1">List of Locations:
        {#await allItemsPromise then items}
        {#each items.data.locations as location}
        <article>
            <a href="{location.id}">{location.name}
        </article>
        {/each}            
        {/await}
    </div>
    <div class="b2">
        {#await allItemsPromise then items}
           <img src="{items.data.locations[1].banner_img}" alt=""> 
        {/await}
    </div>
    <div class="b3">Ad Slideshow1</div>
    <div class="b4">
        {#await allItemsPromise then items}
        <img src="{items.data.locations[1].logo_img}" alt="">
    {/await}
    </div>
    <div class="b5">
        {#await allItemsPromise then items}
            {items.data.locations[1].name}
        {/await}

    </div>
    <div class="b6">
        {#await allItemsPromise then items}
        <p>
            {items.data.locations[1].address1}
            {items.data.locations[1].city},
            {items.data.locations[1].state}
            {items.data.locations[1].zip}
        </p>
        <p>
            {items.data.locations[1].description}
        </p>
        {/await}
    </div>
</section>