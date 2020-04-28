
<script>
  let count = 0;

	function handleClick() {
		count += 1;
	}
</script>



<div class="uk-container">
		<h1>ABOUT</h1>


<button on:click={handleClick}>
	Clicked {count} {count === 1 ? 'time' : 'times'}
</button>



</div>  
