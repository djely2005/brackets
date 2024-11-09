<script>
    let {text, height=$bindable(), width=$bindable(), finalHeight, finalWidth} = $props();
</script>

<div class="xl:rounded-full xl:bg-slate-700 xl:relative xl:flex xl:justify-center xl:items-center xl:text-center w-fit" bind:offsetHeight={height} bind:offsetWidth={width} style:height = '{finalHeight}px' style:width = '{finalWidth}px'>
    <div>

    </div>
    <p class="xl:text-white xl:text-3xl xl:font-bold xl:px-12 xl:py-6">{text}</p>
</div>