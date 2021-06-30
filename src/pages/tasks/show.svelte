<script>
//import {link} from 'svelte-spa-router'
import client from '../../apollo-client'
import { setClient } from "svelte-apollo";
import QGL_TASK from '../../graphql/task';

//
setClient(client);
export let params = Params, item = {}

const  get_item = async function (id){
  var data = await client.query({
    query: QGL_TASK.GET_TASK(id) ,fetchPolicy: "network-only"
  })
  item = data.data.task  
}
console.log(params.id)
get_item(params.id)
</script>

<!-- -->
<div class="container">
	<h3>Tasks - show</h3>
  ID : {params.id}
  <hr />
  {item.title}

</div>
