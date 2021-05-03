<script>
  import { goto } from "$app/navigation";

  import supebase from "$lib/db"
  import {Container} from "projectc-components"

  async function getUsers() {
    return await supebase
      .from("User")
      .select(`
        id,
        name,
        surname,
        function,
        organisation
      `)
  }
</script>

{#await getUsers()}
  <Container size="m">
    <p>Waiting ....</p>
  </Container>
{:then users} 
  {#each users.body as user}
    <div on:click={() => goto(`user/${user.id}`)}>
      <Container size="m" hoverable={true}>
        {user.name} {user.surname} | with function: {user.function}
      </Container>
    </div>
  {/each}
{/await}