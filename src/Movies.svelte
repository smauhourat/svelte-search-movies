<script>
  export let movies = [];
</script>

{#if movies.length == 0}
  <strong>Dont have movies</strong>
{:else}
  {#each movies as { Title, Poster, Year }, index}
    <article>
      <img src={Poster} alt={Title} />
      <h3>{Title}</h3>
      <span>{Year}</span>
      {#if 2022 - Year < 15}
        <i>NEW</i>
      {/if}
    </article>
  {/each}
{/if}

<style>
  i {
    color: red;
  }
  article {
    border: 2px solid #eee;
    border-radius: 4px;
    margin: 10px;
    padding: 16px;
  }
  h3 {
    font-size: 24px;
    margin-bottom: 4px;
  }
</style>
