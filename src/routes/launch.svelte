<script context="module">
    export const load = async({fetch}) => {
        const res = await fetch("https://jsonplaceholder.typicode.com/posts");
        const rockets = await res.json();
        return{
            props:{
                rockets,
            },
        };
    };
</script>

<script>
    import { paginate,LightPaginationNav } from 'svelte-paginate'

    export let rockets;
    let searchTerm = "";

    $: searchedRockets = rockets.filter((rocket) => {
        return rocket.title.includes(searchTerm) || rocket.body.includes(searchTerm);
    });

   

    // let items = rockets.reverse();
    // let currentPage = 1;
    // let pageSize = 4;
    // $: paginatedItems = paginate({items,currentPage,pageSize});
    
</script>
<h1>Data</h1><br>

<input type="text" placeholder="Search By Rocket Name" bind:value={searchTerm}>

<div class="grid grid-cols-2 gap-20 my-10 mx-0">
    {#if searchedRockets.length }
    {#each searchedRockets as item}
        <div class="border p-10 shadow">
            <h2 class="m-0">{item.title.substring(0, 20)}</h2>
            <p>{item.body.substring(0,80)}</p>
            <p class="text-right"><a sveltekit:prefetch class="underline text-blue-900" href={`/data/${item.id}`}>Read More</a></p>
        </div>
    {/each}
    {:else}
        <p>No rockets found with "{searchTerm}"</p>
    {/if}
</div>

<!-- <LightPaginationNav
    totalItems ="{items.length}"
    pageSize = "{pageSize}"
    currentPage = "{currentPage}"
    limit = {"1"}
    showStepOptions = "{true}"
    on:setPage = "{(e) => currentPage = e.detail.page}"
/> -->

<div class="text-center block my-20 mx-auto">
    <h1>Launch</h1>

     <h2 class="no-underline"><a class="text-blue-900" href="/">Home</a></h2>
</div>



