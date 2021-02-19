<script>
  import { onMount, getContext } from "svelte";
  import { jsonData }            from "./store.js";

  import Buscar                  from "./Buscar.svelte";
  import Equipo                from "./Equipo.svelte";
  import Boton                   from "./Boton.svelte";

  const URL = getContext("URL");

  let busqueda = "";
  let equipo = {};

  onMount(async () => {
    const response = await fetch(URL.equipos);
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

<h1>EQUIPOS</h1>
<Buscar bind:busqueda />

<div class="container">
  <Equipo bind:equipo>
    <div style="text-align: right">
      <Boton documento={equipo} tipo="insertar" coleccion="equipos" />
    </div>
  </Equipo>
</div>

<div class="container">
  {#each datos as equipo}
    <Equipo {equipo}>
      <div style="text-align: right">
        <Boton documento={equipo} tipo="modificar" coleccion="equipos" />
        <Boton documento={equipo} tipo="eliminar"  coleccion="equipos" />
      </div>
    </Equipo>
  {/each}
</div>
