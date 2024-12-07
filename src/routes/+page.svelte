<script>
// @ts-nocheck

    let counter = 1; // Página inicial
    let characters = []; // Array de personajes
    let loading = true; // Indicador de carga
    let error = null; // Error en la carga
  
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
  
    // Inicializar carga de personajes
    loadCharacters(counter);
  
    // Función para avanzar de página
    const handleNext = () => {
      counter++;
      loadCharacters(counter);
    };
  
    // Función para retroceder de página
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
    ul {
      list-style: none;
      padding: 0;
    }
    li {
      font-size: 20px;
      margin: 5px 0;
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
    <ul>
      {#each characters as character}
        <li>{character.name}</li>
      {/each}
    </ul>
  {:else}
    <p>No hay personajes para mostrar.</p>
  {/if}
  
  {#if error}
    <p>Error: {error}</p>
  {/if}
  