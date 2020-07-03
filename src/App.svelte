<script>
	import { Router, Link, Route } from "svelte-routing";
	import Questions from "./routes/Questions.svelte";
	import SearchMovies from "./routes/SearchMovies.svelte";
  
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
		<a href="/replace" replace>Replace this URL</a>
		<a href="/native" noroute>Use the native action</a>
		<Link to="/">Questions</Link>
		<Link to="SearchMovies">SearchMovies</Link>
	</nav>
	<div>
		<Route path="/" component={Questions} />
		<Route path="SearchMovies" component={SearchMovies} />
	</div>
</Router>