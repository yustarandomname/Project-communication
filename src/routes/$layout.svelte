<script>
  import { Navigation } from "projectc-components"
  import Login from "$lib/Login.svelte"
  import supabase from "$lib/db"
  import { user } from "$lib/stores/user"

  // When user is chached in browser storage => set user store
  user.set(supabase.auth.user())

  // When auth state changes => update user store
  supabase.auth.onAuthStateChange((event, session) => {
    user.set(session?.user || false)
  })
</script>

<Navigation title={"Project communication"}></Navigation>

{#if $user}
  Signed in as: {$user.email}
  <button on:click={() => supabase.auth.signOut()}>Sign out</button>

  <slot/>
{:else}
  <Login />
{/if}