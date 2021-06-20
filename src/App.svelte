<script>
  import { onMount } from "svelte";

  let results;
  onMount(async () => {
    await fetch(`https://backend-task-incubate.up.railway.app/getData`)
      .then((r) => r.json())
      .then((data) => {
        results = data;
      });
  });
</script>

{#if results}
  <table style="width:100%">
    <tr>
      <th>Full Name</th>
      <th>Email</th>
      <th>Number</th>
      <th>City</th>
      <th>Url</th>
      <th>Team Names</th>
    </tr>
    {#each results as result}
      <tr>
        <td>
          {result.full_name}
        </td>
        <td>
          {result.email}
        </td>
        <td>
          {result.number}
        </td>
        <td>
          {result.city}
        </td>
        <td>
          <a href={result.url}>{result.url}</a>
        </td>
        {#each result.mydata as data}
          {data.team_name}
        {/each}
      </tr>
    {/each}
  </table>
{:else}
  <p class="loading">loading...</p>
{/if}