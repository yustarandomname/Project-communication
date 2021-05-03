<script>
  import { Form, Input } from "projectc-components"
  import supabase from "$lib/db"

  let email;
  let error = false
  let submitMessage = "Login"
  let feedback = false

  async function signIn() {
    [submitMessage, error, feedback] = [false, false, false]

    const { error: err } = await supabase.auth.signIn({
      email: email
    })

    if (err) {
      error = err.message
      submitMessage = "Retry"
    } else {
      error = false
      submitMessage = "Resend"
      feedback = "An email has been send to: " + email
    }
    
  }
  

</script>

<Form size="s" header={"Sign in"} on:submit={signIn} submitMessage={submitMessage} {error} {feedback}>
  <Input.Text placeholder="email" required="true" bind:value={email}/>
</Form>