<script>
  import Movies from "./Movies.svelte";
  let value = "";
  let promise = Promise.resolve([]);

  async function fetchMovies(arg) {
    const response = await self.fetch(
      `https://www.omdbapi.com/?s=cars&apikey=422350ff`
    );

    if (response.ok) {
      return response.json();
    } else {
      throw new Error(`Ha ocurrido un error`);
    }
  }

  const handleInput = (event) => {
    value = event.target.value;
    $: if (value.length > 2) {
      promise = fetchMovies(value);
    }
  };
</script>

<input placeholder="Search movies...." on:input={handleInput} {value} />

{#await promise}
  <strong>Loading.....</strong>
{:then movies}
  <Movies movies={movies.Search} />
{:catch error}
  <p style="color: red">{error.message}</p>
{/await}
