<script>
/* prop */
export let active = false;
export let emailUsuario;


  import { Router, Link, Route } from "svelte-routing";
  import Home from "../routes/Home.svelte";
  import About from "../routes/About.svelte";
  import Blog from "../routes/Blog.svelte";
  import Dashboard from "../routes/Dashboard.svelte";
  export let url = "";
</script>


<Router url="{url}">
<div id="offcanvas-nav" uk-offcanvas="mode: push; overlay: true">
    <div class="uk-offcanvas-bar">
<!-- ? -->
{#if active}
        <img class="uk-preserve-width uk-border-circle" src="https://getuikit.com/docs/images/avatar.jpg" width="40" alt="">
        <p class="uk-align-center">{emailUsuario}</p>
        <hr>
        <ul class="uk-nav uk-nav-default">
            <li class="uk-nav-header">Escritorio</li>
           
            <li class="uk-active"><Link to="/"><span class="uk-margin-small-right" uk-icon="icon: home"></span> Home</Link></li>
            <li class="uk-nav-divider"></li>
            <li><Link to="about"><span class="uk-margin-small-right" uk-icon="icon: happy"></span> About</Link></li>
            <li><Link to="blog"><span class="uk-margin-small-right" uk-icon="icon: server
"></span> Blog</Link></li>
            <!-- <li><Link to="dashboard"><span class="uk-margin-small-right" uk-icon="icon: table"></span> Dashboard</Link></li> -->
        </ul>
{/if}

    </div>
</div>

 <div>
    <Route path="blog" component="{Blog}" />
    <Route path="about" component="{About}" />
    <!-- <Route path="dashboard" component="{Dashboard}" /> -->
    <Route path="/"><Home /></Route>
  </div>
</Router>
