<script context="module">
    export const load = async({fetch,params}) => {
        const id = params.authorId;
        // const res = await fetch("https://jsonplaceholder.typicode.com/users/${id}");
        // const user = await res.json();
     
        // const resRockets = await fetch("https://jsonplaceholder.typicode.com/posts");
        // const allrockets = await resRockets.json();

        const [resUser, resRockets] = await Promise.all([
            fetch("https://jsonplaceholder.typicode.com/users/${id}"),
            fetch("https://jsonplaceholder.typicode.com/posts"),
        ])

        const user = await resUser.json();
        const allrockets = await resRockets.json();

        const rockets = allrockets.filter((rocket) => {
            return rocket.userId === user.id;
        })
        
        return {
            props: {
                user,
                rockets
            },
        };
    };
</script>

<script>
    export let user;
    export let rockets;
</script>



<h1>{user.name}</h1>
<!-- <p>{user.company.catchPhrase}</p> -->
<p>{user.email}</p>

<h2>Rockets search by {user.name}</h2>
<ul>
    {#each rockets as item}
        <li>
            <a href={`/data/${item.id}`}>{item.title}</a>
        </li>
    {/each}
</ul>
