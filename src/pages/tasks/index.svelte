<script>
import {link} from 'svelte-spa-router'
import GQL_TASK from '../../graphql/task';
import client from '../../apollo-client'
import { setClient } from "svelte-apollo";
//
export let items = []
setClient(client);

const  get_items = async function (){
  const data = await client.query({
    query: GQL_TASK.GET_TASKS(), fetchPolicy: "network-only"
  })
  console.log(data.data.tasks) 
  items = data.data.tasks 
}
get_items()
</script>
<!-- -->
<div class="container">
	<h3>Tasks - index</h3>
  <a href="/tasks/create" use:link class="btn btn-primary">Create
  </a>
  <hr />
  {#each items as item}
  <h3><a href={`/tasks/show/${item.id}`} use:link>{item.title}</a>
  </h3>
  <p>ID : {item.id}
    <a href={`/tasks/edit/${item.id}`} use:link class="ml-2 btn btn-outline-primary">
      Edit</a>
  </p>
  <hr />
  {/each}

</div>
