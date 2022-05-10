<script context="module">
	export const prerender = true;
    import UI from "../components/ui.svelte";
</script>

<svelte:head>
    <title>Collatz Conjecture Visualizer</title>
</svelte:head>

<body class="dark:bg-gray-800 dark:text-white">
    <div class="px-4 py-4 w-4/5 m-auto mt-10 text-center">
        <h1 class="text-7xl font-bold">Collatz Conjecture Visualizer</h1>
        <h2 class="text-2xl text-gray-600 dark:text-gray-400">Put in a number. We'll halve it if it's even, and triple it and add one if it's odd. Keep doing that, and it'll <a class="text-blue-600 dark:text-blue-300 hover:underline hover:animate-pulse" href="https://en.wikipedia.org/wiki/Collatz_conjecture" target="_blank">eventually become one</a>. This is plotted to a graph in order to visualize.</h2>
    </div>
    <UI />
</body>