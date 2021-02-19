<script>
  import { Route }  from "svelte-routing";
  import Inicio     from "./Inicio.svelte";
  import Equipos  from "./Equipos.svelte";
  import Jugadores   from "./Jugadores.svelte";
</script>

<style>
  main {
    padding: 20px;
    padding-top: 50px;
  }
</style>

<main id="contenido">
  <Route path="/" component={Inicio} />
  <Route path="/equipos" component={Equipos} />
  <Route path="/jugadores" component={Jugadores} />
</main>
