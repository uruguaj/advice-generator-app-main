<script>
    import './app.css';
    import {useQuery} from "@sveltestack/svelte-query";
    const queryResult = useQuery('advice', () =>
        fetch('https://api.adviceslip.com/advice').then(res =>
            res.json()
        )
    )

    const refetchData = ()=>{
        location.reload();
    }
</script>


<main>
    <div class="box">
        <div class="in-box">
            {#if $queryResult.isLoading}
            <span class="advice">Advice #Loading...</span>
            {:else if $queryResult.error}
                <span class="advice">Error has occurred!.</span>
            {:else}
            <span class="advice">Advice #{$queryResult.data.slip.id}</span>
            {/if}
            {#if $queryResult.isLoading}
                <h1>„
                    Loading...
                    “</h1>
            {:else if $queryResult.error}
                <h1>„
                    Error has occurred! :(
                    “</h1>
            {:else}
            <h1>„
                {$queryResult.data.slip.advice}
                “</h1>
            {/if}
            <img src="/images/pattern-divider-mobile.svg" alt="divider" class="mobile-divider"/>
            <button on:click={refetchData}>
                <img src="/images/icon-dice.svg" alt="button-dice"/>
            </button>
        </div>
    </div>
    <div class="ad">
        <span>If you want to support me check <a href="https://uruguaj.com">uruguaj.com</a></span>
    </div>
</main>
