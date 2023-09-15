<script>
 import './app.css';
 import {onMount} from "svelte";
 let data;
 let id;
 let advice;

 const fetchData = async () =>{
   try {
     const response = await fetch('https://api.adviceslip.com/advice')
     if (response.ok){
       data = await response.json();
       advice = data.slip.advice;
       id = data.slip.id
     }
   } catch (error){
     return alert("Failed to fetch!")
   }

 }
 onMount(fetchData)
 const handleClick =async ()=>{
   try {
     await fetchData();
   } catch (error){
      alert("Error while fetching!")
   }
 }

</script>

<main>
  <div class="box">
    <div class="in-box">
      <span class="advice">Advice #{id}</span>
      <h1>„
        {advice}
        “</h1>
        <img src="/images/pattern-divider-mobile.svg" alt="divider" class="mobile-divider"/>
        <button on:click={handleClick}>
          <img src="/images/icon-dice.svg" alt="button-dice"/>
        </button>
    </div>
  </div>
  <div class="ad">
  <span>If you want to support me check <a href="https://uruguaj.com">uruguaj.com</a></span>
  </div>
</main>