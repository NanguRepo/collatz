<script context="module">
	export const prerender = true;
</script>

<svelte:head>
    <title>Collatz Conjecture Visualizer</title>
</svelte:head>

<script lang="ts">
    import Chart from "../components/chart.svelte"
    const collatz = (n: number) => {
        // create a new array with every value in the collatz conjecture with n as the seed
        const arr = [n]
        while (n > 1) {
            n = n % 2 === 0 ? n / 2 : 3 * n + 1;
            arr.push(n)
        }
        return arr
    }
    let x: number;
    let chartData: Object;
    $: data = collatz(x);
    $: chartData = {
        labels: [...Array(data.length).keys()],
        datasets: [
            {
                label: "Value",
                backgroundColor: "rgba(255,99,132,0.2)",
                borderColor: "rgba(255,99,132,1)",
                borderWidth: 1,
                hoverBackgroundColor: "rgba(255,99,132,0.4)",
                hoverBorderColor: "rgba(255,99,132,1)",
                data: data
            }
        ], 
    }
    
</script>

<div class="bg-slate-200 shadow-lg rounded-lg px-4 py-4 w-4/5 m-auto mt-10 dark:bg-slate-700">
    <div class="pb-10">
        <label for="x">Enter a number:</label>
        <input type="number" class="bg-slate-100 dark:bg-slate-600 rounded ml-1" placeholder="Any positive number" bind:value={x} />
        <button 
            class="rounded bg-slate-300 px-2 hover:bg-slate-400"
            on:click={() => {
                // generate a new random number
                x = Math.floor(Math.random() * 10000)
            }}
        >
            Get a random number
        </button>
    </div>
    <div class="outline-dotted rounded">
        <Chart data={chartData}/>
    </div>
</div>