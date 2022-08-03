<script>
  import { genericDataUrl, fetchAvatar } from "./shared.js";
  // The fetchAvatar action is used on the <img> HTMLImageElement
  //   use:fetchAvatar={ url }
  //
  let disabled = false;
  let promise = Promise.resolve([]);
  let genericAvatar = genericDataUrl();

  async function fetchUsers() {
    const response = await self.fetch(
      "https://api.github.com/users?per_page=5"
    );

    if (response.ok) {
      return response.json();
    } else {
      throw new Error(usersX);
    }
  }

  function handleClick() {
    // Now set it to the real fetch promise
    promise = fetchUsers();
    disabled = true;
  }
</script>

<!-- Stop hitting GitHub on every source edit -->
<button on:click={handleClick} {disabled}> Load Users </button>

{#await promise}
  <p>...waiting</p>
{:then users}
  {#each users as { login, url } (login)}
    <h3>{login}</h3>
    <img height="100" src={genericAvatar} alt={login} use:fetchAvatar={url} />
  {/each}
{:catch error}
  <p style="color: red">{error.message}</p>
{/await}
