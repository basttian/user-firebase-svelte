<script>

import DASHBOARD from './Dashboard.svelte';

/* Observador */
let userActive = false;
let userEmail = '';

$: if (!userActive){

	firebase.auth().onAuthStateChanged(function(user) {
	if (user) {
		// User is signed in.
		var displayName = user.displayName;
		var email = user.email;
		var emailVerified = user.emailVerified;
		var photoURL = user.photoURL;
		var isAnonymous = user.isAnonymous;
		var uid = user.uid;
		var providerData = user.providerData;
        userActive = true;
        userEmail = user.email;
        //console.log(user.email);
        
	} else {
		// User is signed out.
		userActive = false;
	}
	});

}

/* Login Form */
let email = '';
let password = '';

const Acceso = () => {

 firebase.auth().signInWithEmailAndPassword(email, password).catch(function(error) {
  // Handle Errors here.
  var errorCode = error.code;
  var errorMessage = error.message;
   if (errorCode === 'auth/wrong-password') {
            alert('Contraseña incorrecta.');
          } else {
            alert(errorMessage);
          }
});
 email = '';
 password = '';
}

</script>


{#if !userActive}
<div class="uk-section">
    <div class="uk-container">
        <div class="uk-position-center">
		    <div class="uk-card uk-card-default uk-card-hover uk-card-body">
                <h1 class="uk-card-title">¡Hola! Ingresá tu e‑mail</h1>
                <div class="uk-margin">
                    <input type="email" class="uk-input uk-form-width-medium uk-form-large uk-form-width-large" bind:value={email}  placeholder="em@il">
                </div>
                <div class="uk-margin">
                    <input type="password" class="uk-input uk-form-width-medium uk-form-large uk-form-width-large" bind:value={password} placeholder="******">
                </div>
                <p uk-margin>
                    <button class="uk-button uk-button-primary uk-button-large uk-align-center" on:click={Acceso}>Ingresar</button>
                </p>
            </div>
        </div>
    </div>
</div>
{:else}
<DASHBOARD emailUsuario={userEmail} />
{/if}

        

