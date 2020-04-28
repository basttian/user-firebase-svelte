<script>
	import './firebase.js';
	import CAMVAS from './layouts/Offcanvas.svelte';
	import NAVAR from './layouts/Nav.svelte';

let active = false;


$: if (!active){

	firebase.auth().onAuthStateChanged(function(user) {
	if (user) {
		// User is signed in.
		active = true;
	} else {
		// No user is signed in.
		active = false;
	}
	});

}
</script>


<NAVAR active={active} />
<!-- OffCambas Lateral Menu -->
<CAMVAS active={active}/>



