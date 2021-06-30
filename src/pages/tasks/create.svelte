<script>
import Nav from '../../components/Navi.svelte';
import client from '../../apollo-client'
import { setClient } from "svelte-apollo";
import QGL_TASK from '../../graphql/task';

//export let name;
setClient(client);
async function handleClick() {
//  alert('clicked')
  await add_item()
}
async function add_item(){
  try {
    var elemTitle = document.getElementById('title');
    const result = await client.mutate({
      mutation: QGL_TASK.get_gql_add(elemTitle.value)
    }) 
console.log(result)
    window.location.href = '/#/tasks/'
  } catch (error) {
    console.error(error);
  }    
}
</script>

<!-- -->
<div class="container">
	<h3>Tasks - Create111</h3>
  <hr />
  <div class="form-group">
    <label>Title:
      <input type="text" class="form-control" name="title" id="title" />
    </label>
  </div>
  <hr />
  <button on:click={handleClick} class="btn btn-primary">Add</button>
</div>
