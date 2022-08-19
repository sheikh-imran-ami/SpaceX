<script>
  import "../app.css";
  import Title from "../lib/title.svelte";
  import "../styles/global.css";
</script>

<header class="flex justify-center">
  <title title="SpaceX" />
</header>

<main class="max-w-4xl my-20 mx-auto">
  <!-- page content -->

  <slot />
</main>

<footer class="text-center">
  <p>&copy; Copyright 2022 SpaceX</p>
</footer>


