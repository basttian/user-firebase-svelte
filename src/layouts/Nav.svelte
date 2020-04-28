<script>
	export let active = false;
</script>

{#if active}
    <nav class="uk-navbar uk-navbar-container uk-margin">
        <div class="uk-navbar-left">
            <a class="uk-navbar-toggle" href="javascript:void(0)" uk-toggle="target: #offcanvas-nav">
                <span uk-navbar-toggle-icon></span> <span class="uk-margin-small-left">Menu</span>
            </a>
        </div>
    </nav>
{/if}