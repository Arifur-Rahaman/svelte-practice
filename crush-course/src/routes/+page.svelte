<script lang="ts">
    import {globalCount} from '../store'

    const numbers = [1,2,3,4,5,6,7]
    let count = 0;
    let gcount = 0

    const increase = () =>{
        count = count+1
    }
    
    const decrease = () =>{
        count = count-1
    }

    globalCount.subscribe((value)=>{
        gcount = value
    })

    const handleGlobalUpdate = ()=>{
        globalCount.update((value)=>{
            return value+1
        })
    }
    
</script>

<div>
    <h1>Global Count: {gcount}</h1>
    <button on:click={handleGlobalUpdate}>Increase Global</button>
    <h1>{count}</h1>
    <button on:click={increase}>Increase</button>
    <button on:click={decrease}>Decrease</button>
    {#each numbers as number}
        <h1>Hello {number}</h1>
    {/each}
</div>
