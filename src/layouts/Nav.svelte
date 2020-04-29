<script>
	export let active = false;

	const Salir = () => {
		UIkit.modal.confirm('Esta seguro de cerrar la sesion!').then(function() {
			firebase.auth().signOut();
			var notifications = UIkit.notification('Adios!!', 'danger');
	    	console.log('Confirmed.')
		}, function () {
	    	console.log('Rejected.')
		});
	}
</script>

{#if active}
    <nav class="uk-navbar uk-navbar-container uk-margin">
        <div class="uk-navbar-left">
            <a class="uk-navbar-toggle" href="javascript:void(0)" uk-toggle="target: #offcanvas-nav">
                <span uk-navbar-toggle-icon></span> <span class="uk-margin-small-left">Menu</span>
            </a>
        </div>
   
<!-- Right -->
    <div class="uk-navbar-right">
        <ul class="uk-navbar-nav">
            <li>
                 <button class="uk-icon-link uk-margin-small-right" on:click={Salir} uk-icon="sign-out"></button>
            </li>
        </ul>
    </div>
 </nav>
{/if}