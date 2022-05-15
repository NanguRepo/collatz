<script lang="ts">
    import Fa from 'svelte-fa/src/fa.svelte'
    import { faQuestionCircle } from '@fortawesome/free-solid-svg-icons'
    export let data: Array<number>
    $: maxNum = Math.max.apply(Math, data)
    $: sum = data.reduce((acc, n) => acc + n, 0);
    $: threshold = "10";
    $: thresholdNum = parseInt(threshold);
    $: minNum = Math.min.apply(Math, data.filter(n => n > thresholdNum))
    $: maxBelowThreshold = Math.max.apply(Math, data.filter(n => n < thresholdNum))
    $: tooltipVisible = false;
</script>

<div class="bg-slate-300 rounded px-4 py-4 dark:bg-slate-800 w-auto max-w-xs h-full font-mono flex flex-col">
    <h1 class="text-xl font-bold underline">Stats</h1>
    <div class="flex flex-row divide-x">
        <div class="flex flex-col pr-2">
            <p class="font-bold text-center">Peak</p>
            <p>{maxNum}</p>
        </div>
        <div class="flex flex-col px-2">
            <p class="font-bold text-center">Average</p>
            <p>{(sum/data.length).toFixed(2)}</p>
        </div>
        <div class="flex flex-col px-2">
            <div class="flex flex-row">
                <p class="font-bold text-center">Low ></p>
                <span class="ml-2 w-fit max-w-prose h-min px-2 dark:text-white dark:bg-slate-900" contenteditable bind:textContent={threshold} />
            </div>
            <div class="flex flex-row items-center gap-1">
                <p>{minNum == Infinity ? maxBelowThreshold:minNum}</p>
                {#if minNum == Infinity}
                    <div 
                        on:click={() => {tooltipVisible = !tooltipVisible;}}
                    >
                        <Fa icon={faQuestionCircle} />
                    </div>
                {/if}
            </div>
        </div>
    </div>
    {#if tooltipVisible && minNum == Infinity}
        <p class="text-xs break-words w-fit">
            This is the closest value to {threshold}, as no numbers above {threshold} exist on the chart.
        </p>
    {/if}
</div>