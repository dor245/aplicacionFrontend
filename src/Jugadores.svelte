<script>
  import { onMount, getContext } from "svelte";
  import { jsonData }            from "./store.js";

  import Buscar                  from "./Buscar.svelte";
  import Jugador                 from "./Jugador.svelte";
  import Boton                   from "./Boton.svelte";

  const URL = getContext("URL");

  let busqueda = "";
  let jugador = {};

  onMount(async () => {
    const response = await fetch(URL.jugadores);
    const data = await response.json();
    $jsonData = data;
  });

  $: regex = new RegExp(busqueda, "i");
  $: datos = busqueda 
    ? $jsonData.filter(item => regex.test(item.nombre))
    : $jsonData;

</script>

<style>
  .container {
    display: flex;
    flex-direction: row;
    align-items: center;
    justify-content: left;
    flex-wrap: wrap;
  }
</style>

<h1>JUGADORES</h1>
<Buscar bind:busqueda />

<div class="container">
  <Jugador bind:jugador>
    <div style="text-align: right">
      <Boton documento={jugador} tipo="insertar" coleccion="jugadores" />
    </div>
  </Jugador>
</div>

<div class="container">
  {#each datos as jugador}
    <Jugador {jugador}>
      <div style="text-align: right">
        <Boton documento={jugador} tipo="modificar" coleccion="jugadores" />
        <Boton documento={jugador} tipo="eliminar" coleccion="jugadores" />
      </div>
    </Jugador>
  {/each}
</div>