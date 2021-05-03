<script>
  import supabase from "$lib/db"
  import { Container } from "projectc-components"
  import { session } from "$app/stores"
  
  export let size = "full"
  export let bucket = "profile"
  export let file = false

  async function getLogo() {
    const { data, error } = await supabase
      .storage
      .from("sign/" + bucket)
      .download(file + "?token=" + token) 

    console.log(data, error)

    return data
  }
</script>

<style>
  .postionOrg {
    display:flex;
    justify-content: flex-end;
    align-items: center;
  }

  .orgLogo {
    height: 3em;
    width: 3em;
    background: red;
    border-radius: 50%;
    margin-left: 1em;
  }
</style>

<Container {size} hoverable={true}>
  <div class="postionOrg">
    <slot name="name"></slot>
    {#if file}
      {#await getLogo()}
        <div class="orgLogo"></div>
      {:then logo}
        <div class="orgLogo">{logo}</div>
      {/await}
    {/if}
  </div>
</Container>