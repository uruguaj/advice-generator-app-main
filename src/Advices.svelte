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

{#if $queryResult.isLoading}
    <main>
        <div class="box">
            <div class="in-box">
                <span class="advice">Advice # Loading...</span>
                <h1>„
                    Loading...
                    “</h1>
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
{:else if $queryResult.error}
    <main>
        <div class="box">
            <div class="in-box">
                <span class="advice">Advice #0.</span>
                <h1>„
                    Error has occurred! Try reload the page.
                    “</h1>
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
{:else}
<main>
    <div class="box">
        <div class="in-box">
            <span class="advice">Advice #{$queryResult.data.slip.id}</span>
            <h1>„
                {$queryResult.data.slip.advice}
                “</h1>
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
{/if}