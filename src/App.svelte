<script>
	import './firebase.js';
	import CANVAS from './layouts/Offcanvas.svelte';
	import NAVAR from './layouts/Nav.svelte';

//NAVAR
let active = false;
//CANVAS
let emailUsuario ='';

$: if (!active){

	firebase.auth().onAuthStateChanged(function(user) {
	if (user) {
		// User is signed in.
		var displayName = user.displayName;
		var photoURL = user.photoURL;
		var email = user.email;
		active = true;
		emailUsuario = user.email;
	} else {
		// No user is signed in.
		active = false;
	}
	});

}
</script>

    <div class="uk-position-center">
    	<div uk-spinner></div>
    </div>



<NAVAR active={active} />
<!-- OffCambas Lateral Menu -->
<CANVAS 
	active={active} 
	emailUsuario={emailUsuario} />

