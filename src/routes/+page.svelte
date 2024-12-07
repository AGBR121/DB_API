<script>
    // @ts-nocheck
  
    let counter = 1;
    let characters = [];
    let loading = true;
    let error = null;
  
    import Personajes from "./personajes.svelte";
  
    async function loadCharacters(page) {
      loading = true;
      error = null;
      try {
        const response = await fetch(
          `https://dragonball-api.com/api/characters?page=${page}&limit=12`
        );
        if (!response.ok) {
          throw new Error("Error al obtener datos de la API");
        }
        const data = await response.json();
        characters = data.items || [];
      } catch (err) {
        error = err instanceof Error ? err.message : "Error desconocido";
      } finally {
        loading = false;
      }
    }
  
    loadCharacters(counter);
  
    const handleNext = () => {
      counter++;
      loadCharacters(counter);
    };
  
    const handlePrevious = () => {
      if (counter > 1) {
        counter--;
        loadCharacters(counter);
      }
    };
  </script>
  
  <style>
    .body{
        background-color: black;
        margin:0;
    }
    .tittle{
        display: flex;
        justify-content: center;
        margin: 0
    }
    button {
      background-color: aqua;
      border-radius: 10px;
      padding: 10px 20px;
      cursor: pointer;
      margin: 10px;
    }
  
    button:hover {
      background-color: #00d0e8;
    }
  
    button:disabled {
      background-color: lightgray;
      cursor: not-allowed;
    }
  
    h1 {
      color: orangered;
      font-family: "Franklin Gothic Medium", "Arial Narrow", Arial, sans-serif;
      font-size: 50px;
      margin: 0;
    }
  .buttonss{
        display: flex;
        justify-content: center;
  }
    .container {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(400px, 1fr));
  gap: 20px; 
  padding-left: 5%;
}
  </style>
  
  <div class="body">
  <div class="tittle">
    <h1>Dragon Ball API</h1>
  </div>
  
  <div class="buttonss">
    <button on:click={handlePrevious} disabled={counter === 1}>Anterior</button>
    <button on:click={handleNext} disabled={ characters.length<12 }>Siguiente</button>
  </div>
  
  {#if loading}
    <p>Cargando personajes...</p>
  {:else if characters.length > 0}
    <div class="container">
      {#each characters as character}
        <Personajes name={character.name} ki={character.ki} maxKi={character.maxKi} race={character.race} image={character.image} />
      {/each}
    </div>
  {:else}
    <p>No hay personajes para mostrar.</p>
  {/if}
  
  {#if error}
    <p>Error: {error}</p>
  {/if}
  <div class="buttonss">
    <button on:click={handlePrevious} disabled={counter === 1}>Anterior</button>
    <button on:click={handleNext} disabled={characters.length<12}>Siguiente</button>
  </div>
</div>