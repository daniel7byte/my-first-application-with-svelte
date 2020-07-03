<script>
	import { Router, Link, Route } from "svelte-routing";
	import Questions from "./routes/Questions.svelte";
	import SearchMovies from "./routes/SearchMovies.svelte";
	import NotFound from "./routes/NotFound.svelte";
  
	export let url = "";
</script>

<style>
	nav {
		color: aqua;
		background-color: blueviolet;
	}
</style>

<Router url="{url}">
	<nav>
		<Link to="/">Questions</Link>
		<Link to="SearchMovies">SearchMovies</Link>
	</nav>
	<div>
		<Route path="/" component={Questions} />
		<Route path="SearchMovies" component={SearchMovies} />
		<Route component="{NotFound}" ><NotFound url={url} /></Route>
	</div>
</Router>