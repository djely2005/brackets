<script>
    import { onMount } from "svelte";
    import Element from "../lib/com/element.svelte";
    function bracketCalculation(array){
        let howMany;
        loop: for (let index = 0; index < array.length; index++) {
            const element = array[index];
            if(2**index >= array.length){
                howMany = 2**index;
                break loop;
            }
        }
        if(array.length == 0){
            return 0;
        }else{
            return howMany;
        } 
    }
    function getBiggest(array){
        return Math.max.apply(Math, array);
    }
    let teams = $state([
        {text: 'Team1 long name', height: 0, width: 0},
        {text: 'Team2', height: 0, width: 0},
        {text: 'Team3', height: 0, width: 0}
    ]);
    console.log(bracketCalculation(teams));
    let heights = [], widths = [];
    let [finalHeight, finalWidth] = $state(0);
    $effect(()=>{
        teams.forEach(element => {
            heights.push(element.height);
            widths.push(element.width);
        });
        console.log(widths);
        finalHeight = getBiggest(heights);
        finalWidth = getBiggest(widths);
    });
</script>

{#each teams as team}
    <div class="">
        <Element text = {team.text} bind:height = {team.height} bind:width = {team.width} finalWidth = {finalWidth} finalHeight={finalHeight}/>
    </div>
{/each}
