<script>
    let count = 0
    const increaseCount = ()=>{
        count = count+1
    }
</script>
<h1 on:click={increaseCount}>Hello world {count}</h1>
