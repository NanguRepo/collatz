<script lang="ts">
    import Chart from "../components/chart.svelte"
    import Stats from "../components/stats.svelte"
    const collatz = (n: number) => {
        // create a new array with every value in the collatz conjecture with n as the seed
        if (!n) {
            return []
        }
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
    $: chartData = data !== [] ? {
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
        ]
    }:[]
</script>

<div class="bg-slate-200 shadow-lg rounded-lg px-4 py-4 w-11/12 md:w-4/5 h-full m-auto mt-10 dark:bg-slate-700">
    <div class="pb-3 flex flex-row">
        <input type="number" class="bg-slate-100 dark:bg-slate-600 rounded ml-1 py-2 px-4 text-xl max-h-32" placeholder="Any positive number" bind:value={x} />
        <button 
            class="rounded bg-slate-300 hover:bg-slate-400 dark:bg-slate-500 dark:hover:bg-slate-500/75 py-2 px-4 max-h-32"
            on:click={() => {
                // generate a new random number
                x = Math.floor(Math.random() * 10000)
            }}
        >
            Get a random number
        </button>
        <div class="w-auto h-auto ml-auto">
            <Stats data={data}/>
        </div>
    </div>

    <div class="rounded bg-gray-100/50 dark:bg-gray-800/50 w-full h-full">
        <Chart data={chartData}/>
    </div>
</div>