<script>
      import { onMount } from "svelte"; // Importamos onMount un método que utilizaremos para detectar cuándo esta montado el componente.
    
	  // Creamos una constate API con la URL de la API publica
      const API = "https://rickandmortyapi.com/api/character";
    
      // Asignamos la variable "data" y "characters" como arreglos vacíos.
      let data = [];
      let characters = [];
    
      // Utilizamos el método onMount para crear lógica una vez que se haya montado en el DOM el componente
      onMount(async () => {
    	// Creamos un llamado a la API por medio de Fetch
        const res = await fetch(API);
    	// Utilizamos "data" para asignar el resultado de la llamada
        data = await res.json();
    	// Cargamos a characters el resultado de los personajes
        characters = data.results;
      });
    </script>
    
    <!-- // Creamos nuestros estilos para la aplicación -->
    <style>
      .characters {
        width: 100%;
        display: grid;
        grid-template-columns: repeat(5, 1fr);
        grid-gap: 8px;
      }
      figure,
      img {
        width: 100%;
        margin: 0;
      }
    </style>
    
    <!-- // Creamos el bloque de HTML de nuestra aplicación donde estará también la lógica para cada personaje. -->
    <div class="characters">
    	<!-- // En el arreglo de personajes regresamos un personaje e iteramos por cada elemento. -->
      {#each characters as character}
    		<!-- // una vez establecido "character" disponemos de los elementos que tiene este objeto. -->
        <figure>
          <img src={character.image} alt={character.name} />
          <figcaption>{character.name}</figcaption>
        </figure>
    	<!-- // En caso de que no tengamos un resultado de la API, creamos un elemento para mostrar "Loading..." -->
      {:else}
        <p>loading...</p>
      {/each}
    </div>