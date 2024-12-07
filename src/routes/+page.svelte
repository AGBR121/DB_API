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
        const response = await fetch(`https://dragonball-api.com/api/characters?page=${page}&limit=12`);
        if (!response.ok) {
          throw new Error('Error al obtener datos de la API');
        }
        const data = await response.json();
        characters = data.items || [];
      } catch (err) {
        error = err instanceof Error ? err.message : 'Error desconocido';
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
      font-family: 'Franklin Gothic Medium', 'Arial Narrow', Arial, sans-serif;
      font-size: 50px;
      margin: 0;
    }
    .container {
      display: flex;
      justify-content: center;
      margin: 0;
    }
  </style>
  
  <div class="container">
    <h1>Dragon Ball API</h1>
  </div>
  
  <div class="buttons">
    <button on:click={handlePrevious} disabled={counter === 1}>Anterior</button>
    <button on:click={handleNext}>Siguiente</button>
  </div>
  
  {#if loading}
    <p>Cargando personajes...</p>
  {:else if characters.length > 0}
      {#each characters as character}
        <Personajes name={character.name} ki={character.ki} maxKi={character.maxKi} race={character.race}/>
      {/each}
  {:else}
    <p>No hay personajes para mostrar.</p>
  {/if}
  
  {#if error}
    <p>Error: {error}</p>
  {/if}
  