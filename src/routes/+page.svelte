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
        {text: 'Team1 long name', height: 0, width: 0, teamStart: 0, teamState: 0},
        {text: 'Team2', height: 0, width: 0, teamStart: 1, teamState: 2},
        {text: 'Team3', height: 0, width: 0, teamStart: 2, teamState: 1}
    ]);
    let bracketSize = bracketCalculation(teams);
    console.log(bracketSize);
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

    function recursive(numberOfDiv, array){
        if(numberOfDiv > 1){
            numberOfDiv /= 2;
            for (let index = 0; index < numberOfDiv + 1; index++) {
                
            }
            return "<div>"+recursive(numberOfDiv, array)+"</div>"
        }else{

        }
    }
</script>

<div>
    <p></p>
    <p></p>
</div>

<div>
    <div>
        <p></p>
        <p></p>
    </div>
    <div>
        <p></p>
        <p></p>
    </div>
</div>

{#each teams as team}
    
    {#if team.teamStart <=bracketSize / 2 - 1}
        <div class="float-left">
            <Element text = {team.text} bind:height = {team.height} bind:width = {team.width} finalWidth = {finalWidth} finalHeight={finalHeight}/>
        </div>
    {:else}
        <div class="float-right">
            <Element text = {team.text} bind:height = {team.height} bind:width = {team.width} finalWidth = {finalWidth} finalHeight={finalHeight}/>
        </div>
    {/if}
{/each}
