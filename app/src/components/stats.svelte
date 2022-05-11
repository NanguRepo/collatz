<script lang="ts">
    import Fa from 'svelte-fa/src/fa.svelte'
    import { faQuestionCircle } from '@fortawesome/free-solid-svg-icons'
    export let data: Array<number>
    $: maxNum = Math.max.apply(Math, data)
    $: sum = data.reduce((acc, n) => acc + n, 0);
    $: threshold = 10;
    $: minNum = Math.min.apply(Math, data.filter(n => n > threshold))
    $: maxBelowThreshold = Math.max.apply(Math, data.filter(n => n < threshold))
</script>

<div class="bg-slate-300 rounded px-4 py-4 dark:bg-slate-800 w-full h-full font-mono">
    <h1 class="text-xl font-bold underline">Stats</h1>
    <div class="flex flex-row divide-x">
        <div class="flex flex-col pr-2">
            <p class="font-bold text-right">Peak</p>
            <p>{maxNum}</p>
        </div>
        <div class="flex flex-col px-2">
            <p class="font-bold text-center">Average</p>
            <p>{(sum/data.length).toFixed(2)}</p>
        </div>
        <div class="flex flex-col px-2">
            <div class="flex flex-row">
                <p class="font-bold text-left">Low ></p>
                <input type="number" class="ml-2 w-16" bind:value={threshold} />
            </div>
            <div class="flex flex-row">
                <p>{minNum == Infinity ? maxBelowThreshold:minNum}</p>
                <div data-tooltip-target="tooltip-animation">
                    <Fa icon={faQuestionCircle} size="10" />
                </div>
                <div id="tooltip-animation" role="tooltip" class="inline-block absolute invisible z-10 py-2 px-3 text-sm font-medium text-white bg-gray-900 rounded-lg shadow-sm opacity-0 transition-opacity duration-300 tooltip dark:bg-gray-700">
                    Tooltip content
                    <div class="tooltip-arrow" data-popper-arrow></div>
                </div>
            </div>
        </div>
    </div>
</div>