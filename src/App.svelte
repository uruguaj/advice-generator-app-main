<script>
  import { QueryClient, QueryClientProvider } from '@sveltestack/svelte-query'
  import Advices from "./Advices.svelte";
  const queryClient = new QueryClient()
</script>


<QueryClientProvider client={queryClient}>
  <Advices/>
</QueryClientProvider>