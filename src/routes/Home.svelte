<script>

import DASHBOARD from './Dashboard.svelte';

/* Observador */
let userActive = false;


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

let notifications;
async function resetPassword(){
await UIkit.modal.prompt('Ingrese un email valido:', '').then(function(emailAddress) {
    var auth = firebase.auth();
     auth.sendPasswordResetEmail(emailAddress).then(function() {
      // Email sent.
      var notifications = UIkit.notification('Le enviamos un correo para restablecer su contraseña.', 'primary');
    }).catch(function(error) {
      // An error happened.
      var errorCode = error.code;
      var errorMessage = error.message;
      if (errorCode === 'auth/invalid-email') {
        var notifications = UIkit.notification(errorMessage, 'danger');
      }
      
    });

  }).catch(function(error) {
      // An error happened.
      var errorCode = error.code;
      var errorMessage = error.message;
      if (errorCode === 'auth/argument-error') {
        var notifications = UIkit.notification(errorMessage, 'danger');
      }
      
    });
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
                <button class="uk-icon-link uk-margin-small-right" uk-icon="lock" uk-tooltip="Olvide mi contraseña" on:click={resetPassword}></button>
            </div>
        </div>
    </div>
</div>
{:else}
<DASHBOARD />
{/if}

        

