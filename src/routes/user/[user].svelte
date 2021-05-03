<script context="module">
  import supabase from "$lib/db"

  export async function load({ fetch, page }) {
    const user = await supabase
      .from("User")
      .select(`
        id,
        name,
        surname,
        function,
        bio,
        organisation ( * )
      `)
      .eq("id", page.params.user )

    return {
        props: { user: user.data[0] }
    };
  }
</script>

<script>
  import { goto } from '$app/navigation';
  import Organisation from '$lib/Organisation.svelte';
  import { Popup } from "projectc-components"

  export let user;

  let popup = true

  let goHome = () => goto("/")
</script>

<Popup show={popup} on:exit={goHome}>
  <h1>{user.name} {user.surname}</h1>
  <b>Function:</b> {user.function}<br>
  <b>Bio:</b> {user.bio}<br><br>

  <Organisation>
    <div slot="name">{user.organisation.name}</div>
  </Organisation>
</Popup>
