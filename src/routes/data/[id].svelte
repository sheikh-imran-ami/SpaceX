<script context="module">
    export const load = async({fetch,params}) => {
       const id = params.id;
        const res = await fetch(`https://jsonplaceholder.typicode.com/posts/${id}`);
        const data = await res.json();

        const userRes = await fetch(
            `https://jsonplaceholder.typicode.com/users/${data.userId}`
            );

        const user = await userRes.json();
        return {
            props: {
                data,
                user
            },
        };
    };
</script>

<script>
    export let data;
    export let user;
</script>

<h1>{data.title}</h1>
<p>{data.body}</p>
<p>- Written by <a sveltekit:prefetch class="text-blue-900" href={`/authors/${user.id}`}>{user.name}</a></p>

