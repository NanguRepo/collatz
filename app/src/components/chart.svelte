<script lang="ts">
	import Line from "svelte-chartjs/src/Line.svelte"
	export let data: Object = {
            labels: [...Array(10).keys()],
            datasets: [
                {
                    label: "Value",
                    backgroundColor: "rgba(255,99,132,0.2)",
                    borderColor: "rgba(255,99,132,1)",
                    borderWidth: 1,
                    hoverBackgroundColor: "rgba(255,99,132,0.4)",
                    hoverBorderColor: "rgba(255,99,132,1)"
                }
            ]
        };
</script>

<div class="h-full w-full">
  	<Line bind:data={data}/>
</div>