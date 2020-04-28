
<script>

export let emailUsuario;
const Salir = () => {
    firebase.auth().signOut();
    console.log("Cerrar sesion")
}

</script>

<div class="uk-container">
    <h1>DASHBOARD</h1>
    <h3 class="uk-align-center">{emailUsuario}</h3>
    <p uk-margin>
        <button class="uk-button uk-button-secondary" on:click={Salir}>Cerrar sesion</button>
    </p>
























</div>

