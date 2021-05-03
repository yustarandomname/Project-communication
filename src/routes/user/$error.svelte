<script>
  import { goto } from '$app/navigation';
  import { Popup } from "projectc-components"



  let goHome = () => goto("/")
</script>

<Popup show={true} on:exit={goHome}>
  <h1>No user found</h1>
</Popup>