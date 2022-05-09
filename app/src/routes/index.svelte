<div class="bg-slate-200 shadow-lg rounded-lg px-4 py-4 w-fit h-auto m-auto mt-10 dark:bg-slate-700">
    <input type="number" placeholder="num1" bind:value={x} />
    <input type="number" placeholder="num2" bind:value={y} />
    <button 
        class="rounded bg-slate-300 px-2 hover:bg-slate-400"
        on:click={handleClick}
    >find out</button>
    <h1 class="text-2xl break-words">{output}</h1>
</div>

<script lang="ts">
    const isDivisible = (a: number, b: number) => {
        return a % b === 0;
    }
    let x: number = 0;
    let y: number = 0;
    let output: boolean;
    const handleClick = () => {
        output = isDivisible(x, y);
    }
</script>