<script>
  import Movies from "./Movies.svelte";
  let value = "";
  let loading = false;
  let movies = [];

  const handleInput = (event) => {
    value = event.target.value;
    console.log(event.target.value);
    $: if (value.length > 2) {
      loading = true;
      fetch(`https://www.omdbapi.com/?s=${value}&apikey=422350ff`)
        .then((res) => res.json())
        .then((apiRes) => {
          movies = apiRes.Search || [];
          loading = false;
        })
        .catch((error) => (loading = false));
    }
  };
</script>

<input placeholder="Search movies...." on:input={handleInput} {value} />

{#if loading}
  <strong>Loading.....</strong>
{:else if movies.length > 0}
  <Movies {movies} />
{:else}
  <strong>Dont have movies</strong>
{/if}
